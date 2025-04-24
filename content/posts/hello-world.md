+++
date = '2025-04-24T22:39:57+08:00'
draft = false
title = 'Hello World'
+++

今日到达大理后，先游玩大理古城。漫步在古城的各条街道，感受古城的生活气息；之后前往崇圣寺三塔公园，近距离接触大理国时期皇家寺院仅存的古迹；再到三塔南侧的三塔倒影公园，这里可以拍到三塔在水潭里的倒影，最佳拍摄时间是16:00-17:00。傍晚回到大理古城，开始大理的夜生活，夜间的人民路才真正的热闹起来。

今日到达大理后，先游玩大理古城。漫步在古城的各条街道，感受古城的生活气息；之后前往崇圣寺三塔公园，近距离接触大理国时期皇家寺院仅存的古迹；再到三塔南侧的三塔倒影公园，这里可以拍到三塔在水潭里的倒影，最佳拍摄时间是16:00-17:00。傍晚回到大理古城，开始大理的夜生活，夜间的人民路才真正的热闹起来。

今日到达大理后，先游玩大理古城。漫步在古城的各条街道，感受古城的生活气息；之后前往崇圣寺三塔公园，近距离接触大理国时期皇家寺院仅存的古迹；再到三塔南侧的三塔倒影公园，这里可以拍到三塔在水潭里的倒影，最佳拍摄时间是16:00-17:00。傍晚回到大理古城，开始大理的夜生活，夜间的人民路才真正的热闹起来。



```

pyroscope.ebpf "instance" {
 forward_to     = [pyroscope.write.endpoint.receiver]
 targets = discovery.relabel.agent.output
}

pyroscope.scrape "local" {
  forward_to     = [pyroscope.write.endpoint.receiver]
  targets    = [
    {"__address__" = "localhost:12345", "service_name"="grafana/agent"},
  ]
}

pyroscope.write "endpoint" {
 endpoint {
  basic_auth {
   password = "<PASSWORD>"
   username = "<USERNAME>"
  }
  url = "<URL>"
 }
 external_labels = {
  "env"      = "prod",
  "instance" = env("HOSTNAME"),
 }
}
```