%{
  title:  "i3wm And Natural Scrolling",
  date: "Fri 20 Mar 2020 01:15:54 PM CET",
  tags: ["2020", "andi", "linux", "i3"]
}
---


[Since I set up my little Linux box][]- after sticking with Mac for decades -I could manage
a simple and easy setup. The only thing that drives me crazy was the lack of "natural
scrolling."

After a lot of research, try and fail, and hair scrambling, finally, here is how I
managed to get natural scrolling back (for all applications)

First, write a simple shell script.

```bash

# $HOME/bin/natural_scrolling
id=`xinput list | grep -i "Wireless Device Mouse" | cut -d'=' -f2 | cut -d'[' -f1`
echo "Mouse ID $id"

natural_scrolling_id=`xinput list-props ${id} | \
                      grep -i "Natural Scrolling Enabled (" \
                      | cut -d'(' -f2 | cut -d')' -f1`

echo "Natural scrolling ID ${natural_scrolling_id}"

xinput --set-prop $id ${natural_scrolling_id} 1                         

```

And add the following line to your ./config/i3/config

```bash
## Scroll-wheel direction
exec --no-startup-id ~/bin/natural_scrolling
```

To figure out what the name of your pointing device is, do a `xinput list` and watch out
for the name of your device. (Wireless Device Mouse, in the script above, is the value
for my computer. Your device will have another name. Find it out and change the name
in the script.

With that set up, the next time you start i3, natural scrolling should work -naturally.

To enable it without restart, just execute the script `$HOME/bin/natural_scrolling`



[Since I set up my little Linux box]: /2020/andi/linux/2020/02/08/i3wmdesktop.html

