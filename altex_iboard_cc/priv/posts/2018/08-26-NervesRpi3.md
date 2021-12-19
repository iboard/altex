%{
  title: "Elixir, Nerves, Phoenix on A Raspberry Pi",
  author: "Andi",
  date: "Sun Aug 26 20:58:24 CEST 2018",
  tags: [ "2018", "andi", "elixir", "video", "nerves"]
}
---
### Elixir and Nerves is fun!
<iframe width="100%" height="315" src="https://www.youtube.com/embed/1B25N3B2T1Y" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

A Phoenix-Channel listen on messages from web-clients and
switch LEDs on and off.

In the other direction, pressing the button triggers a
Phoenix-channel broadcast to the server, the server randomizes the
three leds and sets them through `Nerves.GPIO`.
Because setting the LED status broadcasts to all web clients,
each display of the buttons on screen is in sync with the LEDs
on Raspberry's breadboard.

Find the source on [Github][]. Also, you can [download the video][]

### A Pretty Strong Team

[Elixir][], [Phoenix-Channels][], and [Nerves][]  

The best thing about [Nerves][] is the way you can update
your raspberry over WiFi without fiddling around with SDCards.
All you have to do is 

      ... code ...
      mix firmware
      mix firmware.push nerves.local
      ... test ...


## Update 2018-08-27

I added a thermometer-circuit and a display for the current temperature
using the PCF8591 A/D-converter.

### Circuit For Button and LEDs

![Circuit for button and leds](/assets/posts/2018/button-and-leds-circuit.png)

### Extended With Circuit For Thermo-resistor And PCF8591

![Extension for thermo-resistor](/assets/posts/2018/thermometer-circuit.png)

The code for the thermo-extension is at [Github-commit](https://github.com/iboard/pocketweb/commit/918eb638a44d08bd3e774ea0922073ff5df86bff)

**A big credit** for [Arkham's Example](https://github.com/Arkham/countermeasures/blob/master/lib/countermeasures.ex)

[Github]: https://github.com/iboard/pocketweb
[download the video]: /assets/posts/2018/Raspberry.mov

[Elixir]: https://elixir-lang.org/
[Phoenix-Channels]: https://hexdocs.pm/phoenix/Phoenix.Channel.html#content
[Nerves]: https://nerves-project.org/


