{
  "dns": {
    "servers": [
      "1.1.1.1",
      "1.0.0.1"
    ],
    "queryStrategy": "UseIP"
  },
  "inbounds": [
    {
      "tag": "socks",
      "port": 10808,
      "listen": "127.0.0.1",
      "protocol": "socks",
      "settings": {
        "udp": true,
        "auth": "noauth"
      },
      "sniffing": {
        "enabled": true,
        "routeOnly": false,
        "destOverride": [
          "http",
          "tls",
          "quic"
        ]
      }
    },
    {
      "tag": "http",
      "port": 10809,
      "listen": "127.0.0.1",
      "protocol": "http",
      "settings": {
        "allowTransparent": false
      },
      "sniffing": {
        "enabled": true,
        "routeOnly": false,
        "destOverride": [
          "http",
          "tls",
          "quic"
        ]
      }
    }
  ],
  "observatory": {
    "enableConcurrency": true,
    "probeInterval": "1m",
    "probeUrl": "https://www.google.com/generate_204",
    "subjectSelector": [
      "tl-10-1-67pe9eae2dk",
      "tl-10-2-rnei9fipkf8"
    ]
  },
  "outbounds": [
    {
      "tag": "tl-10-1-67pe9eae2dk",
      "protocol": "vless",
      "settings": {
        "vnext": [
          {
            "address": "de-new.datanode-internal.net",
            "port": 443,
            "users": [
              {
                "id": "0f6e1194-ab37-4526-8905-307de419e248",
                "encryption": "none",
                "flow": "xtls-rprx-vision"
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "tcp",
        "tcpSettings": {},
        "security": "reality",
        "realitySettings": {
          "serverName": "sun9-37.userapi.com",
          "show": false,
          "publicKey": "r6lN34m1nN-xQZ458j5NPD5xJ3_QBF2bGzY4KJEo4ic",
          "shortId": "abbcd128",
          "fingerprint": "qq"
        }
      }
    },
    {
      "tag": "tl-10-2-rnei9fipkf8",
      "protocol": "vless",
      "settings": {
        "vnext": [
          {
            "address": "res.datanode-internal.net",
            "port": 443,
            "users": [
              {
                "id": "0f6e1194-ab37-4526-8905-307de419e248",
                "encryption": "none",
                "flow": "xtls-rprx-vision"
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "tcp",
        "tcpSettings": {},
        "security": "reality",
        "realitySettings": {
          "serverName": "sun9-37.userapi.com",
          "show": false,
          "publicKey": "r6lN34m1nN-xQZ458j5NPD5xJ3_QBF2bGzY4KJEo4ic",
          "shortId": "abbcd128",
          "fingerprint": "qq"
        }
      }
    },
    {
      "tag": "direct",
      "protocol": "freedom"
    },
    {
      "tag": "block",
      "protocol": "blackhole"
    }
  ],
  "remarks": "🇩🇪 BOOSTX VPN",
  "routing": {
    "domainMatcher": "hybrid",
    "domainStrategy": "IPIfNonMatch",
    "balancers": [
      {
        "tag": "bal_10",
        "selector": [
          "tl-10-1-67pe9eae2dk"
        ],
        "fallbackTag": "tl-10-2-rnei9fipkf8",
        "strategy": {
          "type": "leastLoad",
          "settings": {
            "baselines": [
              "4s"
            ],
            "costs": [
              {
                "match": "tl-10-1-67pe9eae2dk",
                "regexp": false,
                "value": 1
              },
              {
                "match": "tl-10-2-rnei9fipkf8",
                "regexp": false,
                "value": 1000000
              }
            ],
            "expected": 1,
            "maxRTT": "6s"
          }
        }
      }
    ],
    "rules": [
      {
        "type": "field",
        "protocol": [
          "bittorrent"
        ],
        "outboundTag": "block"
      },
      {
        "domain": [
          "domain:mtalk.google.com",
          "domain:push.apple.com",
          "domain:api.push.apple.com"
        ],
        "outboundTag": "direct",
        "type": "field"
      },
      {
        "ip": [
          "17.0.0.0/8"
        ],
        "outboundTag": "direct",
        "type": "field"
      },
      {
        "type": "field",
        "inboundTag": [
          "socks",
          "http"
        ],
        "network": "tcp,udp",
        "balancerTag": "bal_10"
      }
    ]
  }
}
