---
title: Handler Pause And Resume
date: 2016-12-26 11:30:38
tags: Android
categories: Android
---
**在某些特定的情况下，我们可能需要暂停处理MessageQueue中的Message，然后恢复。可以通过一下方法来解决：**

**自定义Handler，复写handleMessage方法，在方法中添加标记位来控制暂停和开始：**


```java

class MyHandler extends Handler {
    Stack<Message> s = new Stack<Message>();
    boolean is_paused = false;

    public synchronized void pause() {
        is_paused = true;
    }

    public synchronized void resume() {
        is_paused = false;
        while (!s.empty()) {
            sendMessageAtFrontOfQueue(s.pop());
        }
    }

    @Override
    public void handleMessage(Message msg) {
        if (is_paused) {
            s.push(Message.obtain(msg));
            return;
        }else{
               super.handleMessage(msg);
               // otherwise handle message as normal
               // ...
        }
    }
    //...
}

```


	