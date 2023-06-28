客户端

```jsonc
{
    "log": {
        "level": "info",
        "timestamp": true
    },
    "route": {
        "rules": [
            {
                "geosite": [
                    "cn",
                    "private"
                ],
                "geoip": [
                    "private"
                ],
                "outbound": "direct"
            }
        ]
    },
    "inbounds": [
        {
            "type": "mixed",
            "tag": "mixed-in",
            "listen": "::",
            "listen_port": 10000,
            "set_system_proxy": false
        }
    ],
    "outbounds": [
        {
            "type": "shadowsocks",
            "tag": "proxy",
            "server": "127.0.0.1",
            "server_port": 80,
            "method": "2022-blake3-aes-128-gcm",
            "password": "3P+xaSaFiXsrQ1KCr2Xvxg==",
            "multiplex": {
                "enabled": true,
                "protocol": "h2mux",
                "max_connections": 4,
                "min_streams": 4,
                "padding": true
            },
            "detour": "socks"
        },
        {
            "type": "socks",
            "tag": "socks",
            "server": "127.0.0.1",
            "server_port": 10808
        },
        {
            "type": "direct",
            "tag": "direct"
        }
    ]
}
```

服务端

```jsonc
{
    "log": {
        "level": "info",
        "timestamp": true
    },
    "inbounds": [
        {
            "type": "shadowsocks",
            "tag": "shadowsocks-in",
            "listen": "127.0.0.1",
            "listen_port": 80,
            "method": "2022-blake3-aes-128-gcm",
            "password": "3P+xaSaFiXsrQ1KCr2Xvxg==" // 执行 openssl rand -base64 16 生成
        }
    ],
    "outbounds": [
        {
            "type": "direct",
            "tag": "direct"
        }
    ]
}
```