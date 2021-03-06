# Hex Plugin

This is the Hex Plugin interface which relies on the HashiCorp Go-Plugin library (https://github.com/hashicorp/go-plugin).

Use this library to implement a plugin for the Hex bot such as with this example:

```
package main

import (
	"github.com/hashicorp/go-plugin"
	"github.com/mmcquillan/hex-plugin"
)

type MyPlugin struct {
}

func (g *MyPlugin) Perform(args hexplugin.Arguments) (resp hexplugin.Response) {
	resp = hexplugin.Response{
		Output:  args.Command,
		Success: true,
	}
	return resp
}

func main() {
	var pluginMap = map[string]plugin.Plugin{
		"action": &hexplugin.HexPlugin{Impl: &MyPlugin{}},
	}
	plugin.Serve(&plugin.ServeConfig{
		HandshakeConfig: hexplugin.GetHandshakeConfig(),
		Plugins:         pluginMap,
	})
}
```
