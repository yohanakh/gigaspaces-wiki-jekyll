---
layout: post102
title:  Monitoring
categories: XAP102ADM
parent: web-management-console.html
weight: 540
---


{% summary %}{% endsummary %}


The `Monitoring` view lets you view `Processing Unit Infrastructure` and  `Processing Unit properties` statistics. XAP provides
default templates for this but all default dashboard templates can be changed. These are located under `[XAP_HOME]/config/webui/dashboards`.

The monitoring view relies on [InfluxDB](http://influxdb.com/). InfluxDB is used to store the time series values that are generated from the XAP infrastructure.
[Grafana](http://grafana.org) is embedded within the XAP web UI and connects to InfluxDB to visualise the time series data that is stored there.


{%note%}
InfluxDB currently runs only on Linux. If you have a repository that runs on Windows, you can implement your own [custom reporter](./metrics-custom-reporter.html) to integrate with the repository.
{%endnote%}


# InfluxDB

Please refer to the InfluxDB website for [installation](http://influxdb.com/docs/v0.8/introduction/installation.html) instructions.
Once InfluxDB is installed you need to create two data bases and then connect XAP to the repositories.  Follow the steps below to configure InfluxDB and connect your XAP environment to it.


### Create the databases

After you installed the InfluxDB, login into the web console and create two data bases that will be used by XAP to store the time series values.

The first data base we will call `metrics` and the second one is called `grafana`.

Creating the databases:

![hosts1.jpg](/attachment_files/web-console/influxdb-create-db.jpg)

<br>

![hosts1.jpg](/attachment_files/web-console/influxdb-create-db2.jpg)

<br>


# Configuration

### Web UI Configuration

By Default InfluxDB uses ports 8083, 8086, 8090, and 8099. This conflicts with the default port for GigaSpaces Web UI Managment Console (8099). If you have Influxdb and XAP WEB UI on the same host you must change the default ports for Influxdb or the WebUI.

{%refer%}
Refer to [Starting the Web Management Console](./web-management-console-starting.html) for more information on the Web UI.
{%endrefer%}

{% inittab starting-stanalone|top %}
{% tabcontent Linux %}

{% highlight console %}

#Specify port via a command line argument
./gs-webui.sh -port 80

#Specify port with a system property
export WEBUI_PORT=80
./gs-webui.sh
{% endhighlight %}

{% endtabcontent %}
{% tabcontent Windows %}

{% highlight console %}
#Specify port via a command line argument
gs-webui.bat -port 80

#Specify port with a system property
set WEBUI_PORT=80
gs-webui.bat
{% endhighlight %}

{% endtabcontent %}
{% endinittab %}


### XAP Configuration

Once the databases are created we need to configure the connection between XAP and InfluxDB. This is done by modifying the `metrics.xml` file which you can find in the XAP distribution
folder `[XAP_HOME]/config/metrics`.

First we configure the reporters:

{%highlight xml%}
<metrics-configuration>
    <reporters>
        <reporter name="influxdb-http">
            <property name="host" value="influxdb-host"/>
            <property name="database" value="metrics"/>
            <property name="username" value="root"/>
            <property name="password" value="root"/>
        </reporter>
    </reporters>
</metrics-configuration>
{%endhighlight%}

{%refer%}
Please refer to the [InfluxDB Reporter](./metrics-influxdb-reporter.html) section for detailed configuration instructions.
{%endrefer%}

Then we configure the dashboard connection for Grafana:

{%highlight xml%}
   <grafana>
        <datasources>
            <datasource name="influxdb">
                <property name="type" value="influxdb"/>
                <property name="url" value="http://influxdb-host:8086/db/metrics"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </datasource>
            <datasource name="grafana">
                <property name="type" value="influxdb"/>
                <property name="url" value="http://influxdb-host:8086/db/grafana"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
                <property name="grafanaDB" value="true"/>
            </datasource>
        </datasources>
    </grafana>
{%endhighlight%}

{%note%}
Please note that Grafana is fully client-side therefore even if InfluxDB is installed on the same host as the web UI the URL needs to be reachable by the client node accessing the UI.
{%endnote%}

Once this configuration is complete and XAP is restarted we are now ready to start visualising our metrics. Our XAP infrastructure should now be connected and writing data to InfluxDB with the default configuration.


# Monitor view

When you open the `Monitor` tab in the XAP web console, you will see the following view:

![hosts1.jpg](/attachment_files/web-console/monitor.jpg)

<br>

# Dashboards

By selecting the folder icon on the right in the menu bar, the available dashboards will be displayed:

![hosts1.jpg](/attachment_files/web-console/monitor1.jpg)

<br>

## Default Space dashboard

![hosts1.jpg](/attachment_files/web-console/monitor2.jpg)

<br>

## Default Processing Unit dashboard

![hosts1.jpg](/attachment_files/web-console/monitor3.jpg)




{%comment%}
This view will be only available if:
1.       Either no secured login performed or in the case of secured login logged in user has both Monitor JVM and Monitor PU permissions.
2.       grafana section in monitoring.xml must be configured to existing running InfluxDb.

Two following dashboards are created for each processing unit:
1.       Processing Unit Infrastructure – exposes VM and LRMI information about vm used by deployed processing unit instances
2.       Processing Unit properties – processing unit information: events information
For each stateful processing unit additional space dashboard created, it exposes space related information: space operations, transactions, connections, replications etc.

All default dashboard templates can be changed and they are located under [XAP_HOME]/config/webui/dashboards, but please note that all changes will be affected only on new deployed processing units, existing and already stored in “grafana” db dashboards will not be changed.

{%endcomment%}

{%refer%}
You can read more in depth about the metrics framework [here](./metrics-overview.html)
{%endrefer%}
