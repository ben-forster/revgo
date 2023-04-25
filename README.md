# revgo

revgo is a Go package for writing bots and self-bots in Revolt easily.

## Features

- Multiple event listen
- Easy to use
- Supports self bots
- Simple cache system

## Installation

- Create a new project and init go.mod file. `go mod init example`
- Install the package using `go get github.com/ben-forster/revgo`

## API Reference

Click [here](https://pkg.go.dev/github.com/ben-forster/revgo@v0.0.1) for api reference.

## Notice

Please note that you will need the Go 1.20 to use revoltgo.

This package is still under development and while you can create a working bot, the library is not finished. Create an issue if you would like to contribute.

## Ping Pong Example (Bot)

```go
package main

import (
    "os"
    "os/signal"
    "syscall"

    "github.com/ben-forster/revgo"
)

func main() {
    // Init a new client.
    client := revgo.Client{
        Token: "bot token",
    }

    // Listen a on message event.
    client.OnMessage(func(m *revgo.Message) {
        if m.Content == "!ping" {
            sendMsg := &revgo.SendMessage{}
            sendMsg.SetContent("🏓 Pong!")

            m.Reply(true, sendMsg)
        }
    })

    // Start the client.
    client.Start()

    // Wait for close.
    sc := make(chan os.Signal, 1)

    signal.Notify(
        sc,
        syscall.SIGINT,
        syscall.SIGTERM,
        os.Interrupt,
    )
    <-sc

    // Destroy client.
    client.Destroy()
}

```

## Ping Pong Example (Self-Bot)

```go
package main

import (
    "os"
    "os/signal"
    "syscall"

    "github.com/ben-forster/revgo"
)

func main() {
    // Init a new client.
    client := revgo.Client{
        SelfBot: &revgo.SelfBot{
            Id:           "session id",
            SessionToken: "session token",
            UserId:       "user id",
        },
    }

    // Listen a on message event.
    client.OnMessage(func(m *revgo.Message) {
        if m.Content == "!ping" {
            sendMsg := &revgo.SendMessage{}
            sendMsg.SetContent("🏓 Pong!")

            m.Reply(true, sendMsg)
        }
    })

    // Start the client.
    client.Start()

    // Wait for close.
    sc := make(chan os.Signal, 1)

    signal.Notify(
        sc,
        syscall.SIGINT,
        syscall.SIGTERM,
        os.Interrupt,
    )
    <-sc

    // Destroy client.
    client.Destroy()
}

```

## To-Do
- [x] OnReady
- [x] OnMessage
- [x] OnMessageUpdate
- [ ] OnMessageAppend
- [ ] OnMessageDelete
- [x] OnChannelCreate
- [x] OnChannelUpdate
- [x] OnChannelDelete
- [ ] OnChannelGroupJoin
- [ ] OnChannelGroupLeave
- [ ] OnChannelStartTyping
- [ ] OnChannelStopTyping
- [ ] OnChannelAck
- [x] OnServerCreate
- [x] OnServerUpdate
- [ ] OnServerDelete
- [ ] OnServerMemberUpdate
- [ ] OnServerMemberJoin
- [ ] OnServerMemberLeave
- [ ] OnServerRoleUpdate
- [ ] OnServerRoleDelete
- [ ] OnUserUpdate
- [ ] OnUserRelationship
- [ ] OnUserRelationship
- [ ] OnEmojiCreate
- [ ] OnEmojiDelete
