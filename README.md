# go-fcm
Firebase Cloud Messaging ( FCM ) Library using golang ( Go )

This library uses HTTP/JSON Firebase Cloud Messaging connection server protocol


###### features

* send messages to a topic
* send messages to a device list
* message can be a notification or data payload



###### in progress
* retry
* instance id features



## Usage



```
go get github.com/NaySoftware/go-fcm

```

### Notes


serverKey is the server key by Firebase Cloud Messaging
to get the key go to :
Firebase project settings --> Cloud Messaging --> then copy the server key


# Examples

### Send to A topic

```golang

package main

import (
	"fmt"
  "github.com/NaySoftware/go-fcm"
)

const (
	 serverKey = "YOUR-KEY"
   topic = "/topics/someTopic"
)

func main() {

	data := map[string]string{
		"msg": "Hello World1",
		"sum": "Happy Day",
	}

	c := fcm.NewFcmClient(serverKey)
	c.NewFcmMsgTo(topic, data)

	status, err := c.Send(1)

	if err == nil {
    status.PrintResults()
	} else {
		fmt.Println(err)
	}

}


```


### Send to a list of Devices (tokens)

```golang

package main

import (
	"fmt"
  "github.com/NaySoftware/go-fcm"
)

const (
	 serverKey = "YOUR-KEY"
)

func main() {

	data := map[string]string{
		"msg": "Hello World1",
		"sum": "Happy Day",
	}

  ids := []string{
      "token1",
  }


  xds := []string{
      "token5",
      "token6",
      "token7",
  }

	c := fcm.NewFcmClient(serverKey)
  c.NewFcmRegIdsMsg(ids, data)
  c.AppendDevices(xds)

	status, err := c.Send(1)

	if err == nil {
    status.PrintResults()
	} else {
		fmt.Println(err)
	}

}



```
