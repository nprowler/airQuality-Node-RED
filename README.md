# airQuality-Node-RED

---

Title: Air Quality index
---
### Problem
Due to the hug amount from forest fires in the area of Calgary. Hitting all time highs of 10+ 
or 'Very High Risk' in air quality index due to smoke. I wanted a gauge on my node-red dashboard.

### Solution
Check every 10 min "https://weather.gc.ca/airquality/pages/abaq-002_e.html" website and extract the
index and show it on a gauge and chart.

{% raw %}
~~~json
[
    {
        "id": "ea1fdbc1.867118",
        "type": "http request",
        "z": "bc1d0805.7db7c8",
        "name": "",
        "method": "GET",
        "ret": "txt",
        "url": "https://weather.gc.ca/airquality/pages/abaq-002_e.html",
        "tls": "",
        "x": 170,
        "y": 2700,
        "wires": [
            [
                "dd86f2c.428551"
            ]
        ]
    },
    {
        "id": "8aacbe7a.3f09a",
        "type": "inject",
        "z": "bc1d0805.7db7c8",
        "name": "",
        "topic": "",
        "payload": "",
        "payloadType": "date",
        "repeat": "600",
        "crontab": "",
        "once": true,
        "onceDelay": "30",
        "x": 170,
        "y": 2660,
        "wires": [
            [
                "ea1fdbc1.867118"
            ]
        ]
    },
    {
        "id": "dd86f2c.428551",
        "type": "html",
        "z": "bc1d0805.7db7c8",
        "name": "Find Data",
        "property": "payload",
        "outproperty": "payload",
        "tag": ".indexBarWithInvisibleBorders p.withBorder",
        "ret": "text",
        "as": "multi",
        "x": 160,
        "y": 2740,
        "wires": [
            [
                "47a3e7bf.b986e8"
            ]
        ]
    },
    {
        "id": "8abeba69.fd18f8",
        "type": "ui_gauge",
        "z": "bc1d0805.7db7c8",
        "name": "",
        "group": "199ea6fd.df9579",
        "order": 3,
        "width": 0,
        "height": 0,
        "gtype": "gage",
        "title": "Air Quality",
        "label": "units",
        "format": "{{payload}}",
        "min": 0,
        "max": 10,
        "colors": [
            "#0cb300",
            "#e6e600",
            "#ca3838"
        ],
        "seg1": "",
        "seg2": "",
        "x": 170,
        "y": 2820,
        "wires": []
    },
    {
        "id": "b8160c5b.dcf1f",
        "type": "ui_chart",
        "z": "bc1d0805.7db7c8",
        "name": "",
        "group": "199ea6fd.df9579",
        "order": 4,
        "width": 0,
        "height": 0,
        "label": "chart",
        "chartType": "line",
        "legend": "false",
        "xformat": "HH:mm:ss",
        "interpolate": "linear",
        "nodata": "",
        "dot": false,
        "ymin": "",
        "ymax": "",
        "removeOlder": 1,
        "removeOlderPoints": "",
        "removeOlderUnit": "3600",
        "cutout": 0,
        "useOneColor": false,
        "colors": [
            "#1f77b4",
            "#aec7e8",
            "#ff7f0e",
            "#2ca02c",
            "#98df8a",
            "#d62728",
            "#ff9896",
            "#9467bd",
            "#c5b0d5"
        ],
        "useOldStyle": false,
        "x": 150,
        "y": 2860,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "e67c2851.fe1b28",
        "type": "comment",
        "z": "bc1d0805.7db7c8",
        "name": "Air Quality",
        "info": "",
        "x": 180,
        "y": 2620,
        "wires": []
    },
    {
        "id": "47a3e7bf.b986e8",
        "type": "function",
        "z": "bc1d0805.7db7c8",
        "name": "Make Payload",
        "func": "var str = msg.payload;\nmsg.payload = str.slice(0, 1); \nmsg.topic = \"Air\";\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 180,
        "y": 2780,
        "wires": [
            [
                "8abeba69.fd18f8",
                "b8160c5b.dcf1f"
            ]
        ]
    },
    {
        "id": "199ea6fd.df9579",
        "type": "ui_group",
        "z": "",
        "name": "Outside",
        "tab": "1924ee6.9de3a92",
        "order": 6,
        "disp": false,
        "width": "6"
    },
    {
        "id": "1924ee6.9de3a92",
        "type": "ui_tab",
        "z": "d22d15d9.90ac38",
        "name": "Temperatures",
        "icon": "fa-thermometer-half",
        "order": 2
    }
]
~~~
{: .flow}
{% endraw %}
