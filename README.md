# OpenWRT-netdata-HA
使用netdata获取数据在homeassistant中展示

sensor:
  - platform: netdata
    host: "192.168.1.1"  #openwrt ip地址
    port: "19999"        #netdata端口号
    name: "ImmortalWrt"  #设备hostname，如果有自定义将下方immortalwrt全部修改为你的hostname

  - platform: template
    sensors:
      immortalwrt_tx_mb:
        friendly_name: "ImmortalWrt上传速度(MB/s)"
        unit_of_measurement: "MB/s"
        value_template: "{{ (states('sensor.immortalwrt_eth1_tx') | float / 8 / 1000) | abs | round(2) }}"    #我是默认eth1为wan口，如果监控别的网口，自定义更换

      immortalwrt_rx_mb:
        friendly_name: "ImmortalWrt下载速度(MB/s)"
        unit_of_measurement: "MB/s"
        value_template: "{{ (states('sensor.immortalwrt_eth1_rx') | float / 8 / 1000) | abs | round(2) }}"    #我是默认eth1为wan口，如果监控别的网口，自定义更换
