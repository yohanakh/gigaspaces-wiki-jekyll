---
layout: post100
title:  Event Processing
categories: XAP100NET
parent: programmers-guide.html
weight: 1100
---

<br>

{%section%}
{%column width=10% %}
![Events-Message.jpg](/attachment_files/subject/Events-Message.png)
{%endcolumn%}
{%column width=90% %}
This section will guide you through event processing APIs and configuration on top of the space.
{%endcolumn%}
{%endsection%}


<br>

{%fpanel%}

[Event Listener Container](./event-listener-container.html){%wbr%}
IEventListenerContainer is an interface that represents an abstraction for subscribing to, and receiving events over a space proxy.

[Notify Container](./notify-container.html){%wbr%}
The notify event container wraps the space data event session API with event container abstraction.

[Polling Container](./polling-container.html){%wbr%}
Allows you to perform polling receive operations against the space.

[FIFO Ordering](./fifo-overview.html){%wbr%}
XAP supports both non-ordered Entries and FIFO ordered Entries when performing space operations.

{%endfpanel%}



