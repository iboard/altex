%{
title: "Bucketier, My First hex.pm Contribution",
author: "Andi",
date: "Sat Jul 21 18:02:18 CEST 2018",
tags: ["2018", "dev", "andi", "elixir", "project", "bucketier", "hex"]
}
---
Today, I wrote my first HEX-package and published it on "hex.pm".
It is an extract of my daily work and was part of an "Umbrella-App" initially.

It is in a very early stage, and a lot of work will be necessary to make it a mature and useful contribution. But, wait and see ;-)


  * [Bucketier at hex.pm](https://hex.pm/packages/bucketier)
  * [Bucketier at Github](https://github.com/iboard/bucketier)

## Usage

```
Bucket.bucket("shopping list")
 |> Bucket.put(1, "Milk")
 |> Bucket.put(2, "Bread")
 |> Bucket.commit()

Bucket.bucket("shopping list")
# %Bucket{name: "shopping list", data: %{1 => "Milk", 2 => "Bread"}}

Bucket.get("shopping list", 1)
# "Milk"

Bucket.values("shopping list")
# ["Milk", "Bread"]

Bucket.keys("shopping list")
# [1,2]
```

The keys, of course, can be anything. It is not restricted to integers.
