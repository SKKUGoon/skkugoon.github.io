---
layout: post
title:  "PROJECT-02. Inter-Market Crypto Trading Bot."
date:   2022-03-15 12:00:00 +0900
categories: Trading Project
---

# Project Inter-Market Crypto Trading Bot

## Websocket Backend in Python 3

<p>
기존 python 3으로 짠 코드는 다음과 같다. 현재 쓰고 있는 프로그램이고
해당 블로그는 전략 같은 것은 다루지 않을 것이므로, 
보안상 중요한 부분들은 ellipsis 처리를 가한다.
</p>

```
from settings import wssmsg as wssmsgs
from settings import sysmsg as sysmsgs

import websockets
import asyncio
import json
import copy

PORT = 7890

print(f"Server listening on port: {PORT}")

backoffice = set()
middleoffice = set()
frontoffice = set()
discordoffice = set()
```

```
async def echo(websocket, path):
    print(sysmsgs.BROADCAST_TOTL_SIG0)
    try:
        async for message in websocket:
            m = json.loads(message)
```
```
            if m['signal_type'] == 'init':
                department = m['data']['dep']
                if department == 'back':
                    print(sysmsgs.BROADCAST_BACK_SIG0)
                    backoffice.add(websocket)
                elif department == 'midl':
                    print(sysmsgs.BROADCAST_MIDD_SIG0)
                    middleoffice.add(websocket)
                else:
                    print(sysmsgs.BROADCAST_FRNT_SIG0)
                    frontoffice.add(websocket)

            # CONNECTION TEST SIGNALS
            elif m['signal_type'] == 'conn':
                print(sysmsgs.BROADCAST_BACK_SIG2)
                ...
            elif m['signal_type'] == 'active':
                print(sysmsgs.BROADCAST_TOTL_SIG2)
                # LOG PAYLOAD
                ...

                # ANS PAYLOAD
                ...

            # TRADE SIGNALS
            elif m['signal_type'] == 'spot_trade':
                # spot trading actions
                ...

            elif m['signal_type'] == 'spread_trade':
                # spread trading actions
                ...

            elif m['signal_type'] == 'test_trade':
                # test trade on testnet
                ...

            else:
                await websocket.send("m")
```

```
    except Exception as e:
        print(e)
        print(sysmsgs.BROADCAST_TOTL_SIG1)

    finally:
        if websocket in backoffice:
            backoffice.remove(websocket)
            print(sysmsgs.BROADCAST_BACK_SIG1)
        elif websocket in middleoffice:
            middleoffice.remove(websocket)
            print(sysmsgs.BROADCAST_MIDD_SIG1)
        else:
            frontoffice.remove(websocket)
            print(sysmsgs.BROADCAST_FRNT_SIG1)

```


```
def broadcast():
    start_server = websockets.serve(echo, "localhost", PORT)

    asyncio.get_event_loop().run_until_complete(start_server)
    asyncio.get_event_loop().run_forever()


if __name__ == "__main__":
    broadcast()
```

## Websocket Backend in Go

```
package main

import (
	"fmt"
	"github.com/gorilla/websocket"
	"log"
	"net/http"
)

import (
	_ "github.com/gorilla/websocket"
)

var upgrader = websocket.Upgrader{
	ReadBufferSize:  1024,
	WriteBufferSize: 1024,
}

func homePage(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Home Page")
}

func wsEndpoint(w http.ResponseWriter, r *http.Request) {
	upgrader.CheckOrigin = func(r *http.Request) bool {
		return true
	}

	ws, err := upgrader.Upgrade(w, r, nil)
	if err != nil {
		log.Println(err)
	}
	log.Println("Client Connected")
	reader(ws)
}

func reader(conn *websocket.Conn) {
	for {
		messageType, p, err := conn.ReadMessage()
		if err != nil {
			log.Println(err)
			return
		}

		fmt.Println(string(p))

		if err := conn.WriteMessage(messageType, p); err != nil {
			log.Println(err)
			return
		}
	}
}

func setupRoutes() {
	http.HandleFunc("/", homePage)
	http.HandleFunc("/ws", wsEndpoint)
}

func main() {
	fmt.Println("Hello World")
	setupRoutes()
	log.Fatal(http.ListenAndServe(":7890", nil))
}

```

