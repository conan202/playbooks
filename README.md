# playbooks
Repositorio de playbooks de Conatel Digital Hub

## Configuración en `xml` de un Router IOS-XR

```xml
<data xmlns="urn:ietf:params:xml:ns:netconf:base:1.0" xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0">
  <aaa xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-aaa-locald-admin-cfg">
    <usernames>
      <username>
        <name>cisco</name>
        <secret>
          <type>type5</type>
          <secret5>$1$d3yh$qn3D8e6MCD3D879N8AkkJ1</secret5>
        </secret>
      </username>
      <username>
        <name>conatel</name>
        <usergroup-under-usernames>
          <usergroup-under-username>
            <name>root-system</name>
          </usergroup-under-username>
        </usergroup-under-usernames>
        <secret>
          <type>type5</type>
          <secret5>$1$PsTy$DGOTYW2O.duf.HzD..3DD.</secret5>
        </secret>
      </username>
    </usernames>
  </aaa>
  <crypto xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-crypto-sam-cfg">
    <ssh xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-crypto-ssh-cfg">
      <server>
        <v2/>
        <netconf-vrf-table>
          <vrf>
            <vrf-name>default</vrf-name>
            <enable/>
          </vrf>
        </netconf-vrf-table>
      </server>
    </ssh>
  </crypto>
  <interface-configurations xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ifmgr-cfg">
    <interface-configuration>
      <active>act</active>
      <interface-name>Loopback0</interface-name>
      <interface-virtual/>
      <ipv4-network xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ipv4-io-cfg">
        <addresses>
          <primary>
            <address>1.1.1.1</address>
            <netmask>255.255.255.255</netmask>
          </primary>
        </addresses>
      </ipv4-network>
    </interface-configuration>
    <interface-configuration>
      <active>act</active>
      <interface-name>MgmtEth0/0/CPU0/0</interface-name>
      <shutdown/>
    </interface-configuration>
    <interface-configuration>
      <active>act</active>
      <interface-name>GigabitEthernet0/0/0/0</interface-name>
      <ipv4-network xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ipv4-io-cfg">
        <addresses>
          <primary>
            <address>10.0.100.50</address>
            <netmask>255.255.0.0</netmask>
          </primary>
        </addresses>
      </ipv4-network>
    </interface-configuration>
    <interface-configuration>
      <active>act</active>
      <interface-name>GigabitEthernet0/0/0/1</interface-name>
      <ipv4-network xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ipv4-io-cfg">
        <addresses>
          <primary>
            <address>192.168.1.1</address>
            <netmask>255.255.255.0</netmask>
          </primary>
        </addresses>
      </ipv4-network>
    </interface-configuration>
    <interface-configuration>
      <active>act</active>
      <interface-name>GigabitEthernet0/0/0/2</interface-name>
      <shutdown/>
    </interface-configuration>
  </interface-configurations>
  <bfd xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ip-bfd-cfg">
    <global-ipv4-echo-source>192.168.1.1</global-ipv4-echo-source>
  </bfd>
  <router-static xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ip-static-cfg">
    <default-vrf>
      <address-family>
        <vrfipv4>
          <vrf-unicast>
            <vrf-prefixes>
              <vrf-prefix>
                <prefix>0.0.0.0</prefix>
                <prefix-length>0</prefix-length>
                <vrf-route>
                  <vrf-next-hop-table>
                    <vrf-next-hop-next-hop-address>
                      <next-hop-address>10.0.0.1</next-hop-address>
                    </vrf-next-hop-next-hop-address>
                  </vrf-next-hop-table>
                </vrf-route>
              </vrf-prefix>
              <vrf-prefix>
                <prefix>192.168.1.2</prefix>
                <prefix-length>32</prefix-length>
                <vrf-route>
                  <vrf-next-hop-table>
                    <vrf-next-hop-next-hop-address>
                      <next-hop-address>192.168.1.2</next-hop-address>
                    </vrf-next-hop-next-hop-address>
                  </vrf-next-hop-table>
                </vrf-route>
              </vrf-prefix>
            </vrf-prefixes>
          </vrf-unicast>
        </vrfipv4>
      </address-family>
    </default-vrf>
  </router-static>
  <bgp xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-ipv4-bgp-cfg">
    <instance>
      <instance-name>default</instance-name>
      <instance-as>
        <as>0</as>
        <four-byte-as>
          <as>65501</as>
          <bgp-running/>
          <default-vrf>
            <global>
              <router-id>1.1.1.1</router-id>
              <global-afs>
                <global-af>
                  <af-name>ipv4-unicast</af-name>
                  <enable/>
                  <sourced-networks>
                    <sourced-network>
                      <network-addr>1.1.1.1</network-addr>
                      <network-prefix>32</network-prefix>
                    </sourced-network>
                  </sourced-networks>
                </global-af>
              </global-afs>
            </global>
            <bgp-entity>
              <neighbor-groups>
                <neighbor-group>
                  <neighbor-group-name>telefonica_test</neighbor-group-name>
                  <create/>
                  <remote-as>
                    <as-xx>0</as-xx>
                    <as-yy>65501</as-yy>
                  </remote-as>
                  <timers>
                    <keepalive-interval>10</keepalive-interval>
                    <hold-time>30</hold-time>
                  </timers>
                  <update-source-interface>GigabitEthernet0/0/0/1</update-source-interface>
                  <neighbor-group-afs>
                    <neighbor-group-af>
                      <af-name>ipv4-unicast</af-name>
                      <activate/>
                      <soft-reconfiguration>
                        <inbound-soft>true</inbound-soft>
                        <soft-always>true</soft-always>
                      </soft-reconfiguration>
                    </neighbor-group-af>
                  </neighbor-group-afs>
                </neighbor-group>
              </neighbor-groups>
              <neighbors>
                <neighbor>
                  <neighbor-address>192.168.1.2</neighbor-address>
                  <neighbor-group-add-member>telefonica_test</neighbor-group-add-member>
                  <bfd-enable-modes>default</bfd-enable-modes>
                  <bfd-multiplier>7</bfd-multiplier>
                  <bfd-minimum-interval>6500</bfd-minimum-interval>
                  <neighbor-afs>
                    <neighbor-af>
                      <af-name>ipv4-unicast</af-name>
                      <activate/>
                    </neighbor-af>
                  </neighbor-afs>
                </neighbor>
              </neighbors>
            </bgp-entity>
          </default-vrf>
        </four-byte-as>
      </instance-as>
    </instance>
  </bgp>
  <netconf-yang xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-man-netconf-cfg">
    <agent>
      <ssh>
        <enable/>
      </ssh>
      <session>
        <limit>50</limit>
      </session>
    </agent>
  </netconf-yang>
  <netconf xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-man-xml-ttyagent-cfg">
    <agent>
      <tty>
        <enable/>
      </tty>
    </agent>
  </netconf>
  <routing-policy xmlns="http://cisco.com/ns/yang/Cisco-IOS-XR-policy-repository-cfg">
    <route-policies>
      <route-policy>
        <route-policy-name>pass-all</route-policy-name>
        <rpl-route-policy>route-policy pass-all  passend-policy</rpl-route-policy>
      </route-policy>
    </route-policies>
  </routing-policy>
  <interfaces xmlns="http://openconfig.net/yang/interfaces">
    <interface>
      <name>Loopback0</name>
      <config>
        <name>Loopback0</name>
        <type xmlns:idx="urn:ietf:params:xml:ns:yang:iana-if-type">idx:softwareLoopback</type>
        <enabled>true</enabled>
      </config>
      <subinterfaces>
        <subinterface>
          <index>0</index>
          <ipv4 xmlns="http://openconfig.net/yang/interfaces/ip">
            <addresses>
              <address>
                <ip>1.1.1.1</ip>
                <config>
                  <ip>1.1.1.1</ip>
                  <prefix-length>32</prefix-length>
                </config>
              </address>
            </addresses>
          </ipv4>
        </subinterface>
      </subinterfaces>
    </interface>
    <interface>
      <name>MgmtEth0/0/CPU0/0</name>
      <config>
        <name>MgmtEth0/0/CPU0/0</name>
        <type xmlns:idx="urn:ietf:params:xml:ns:yang:iana-if-type">idx:ethernetCsmacd</type>
        <enabled>false</enabled>
      </config>
      <ethernet xmlns="http://openconfig.net/yang/interfaces/ethernet">
        <config>
          <auto-negotiate>false</auto-negotiate>
        </config>
      </ethernet>
    </interface>
    <interface>
      <name>GigabitEthernet0/0/0/0</name>
      <config>
        <name>GigabitEthernet0/0/0/0</name>
        <type xmlns:idx="urn:ietf:params:xml:ns:yang:iana-if-type">idx:ethernetCsmacd</type>
        <enabled>true</enabled>
      </config>
      <ethernet xmlns="http://openconfig.net/yang/interfaces/ethernet">
        <config>
          <auto-negotiate>false</auto-negotiate>
        </config>
      </ethernet>
      <subinterfaces>
        <subinterface>
          <index>0</index>
          <ipv4 xmlns="http://openconfig.net/yang/interfaces/ip">
            <addresses>
              <address>
                <ip>10.0.100.50</ip>
                <config>
                  <ip>10.0.100.50</ip>
                  <prefix-length>16</prefix-length>
                </config>
              </address>
            </addresses>
          </ipv4>
        </subinterface>
      </subinterfaces>
    </interface>
    <interface>
      <name>GigabitEthernet0/0/0/1</name>
      <config>
        <name>GigabitEthernet0/0/0/1</name>
        <type xmlns:idx="urn:ietf:params:xml:ns:yang:iana-if-type">idx:ethernetCsmacd</type>
        <enabled>true</enabled>
      </config>
      <ethernet xmlns="http://openconfig.net/yang/interfaces/ethernet">
        <config>
          <auto-negotiate>false</auto-negotiate>
        </config>
      </ethernet>
      <subinterfaces>
        <subinterface>
          <index>0</index>
          <ipv4 xmlns="http://openconfig.net/yang/interfaces/ip">
            <addresses>
              <address>
                <ip>192.168.1.1</ip>
                <config>
                  <ip>192.168.1.1</ip>
                  <prefix-length>24</prefix-length>
                </config>
              </address>
            </addresses>
          </ipv4>
        </subinterface>
      </subinterfaces>
    </interface>
    <interface>
      <name>GigabitEthernet0/0/0/2</name>
      <config>
        <name>GigabitEthernet0/0/0/2</name>
        <type xmlns:idx="urn:ietf:params:xml:ns:yang:iana-if-type">idx:ethernetCsmacd</type>
        <enabled>false</enabled>
      </config>
      <ethernet xmlns="http://openconfig.net/yang/interfaces/ethernet">
        <config>
          <auto-negotiate>false</auto-negotiate>
        </config>
      </ethernet>
    </interface>
  </interfaces>
  <lacp xmlns="http://openconfig.net/yang/lacp">
    <interfaces>
      <interface>
        <name>Loopback0</name>
        <config>
          <name>Loopback0</name>
        </config>
      </interface>
      <interface>
        <name>MgmtEth0/0/CPU0/0</name>
        <config>
          <name>MgmtEth0/0/CPU0/0</name>
        </config>
      </interface>
      <interface>
        <name>GigabitEthernet0/0/0/0</name>
        <config>
          <name>GigabitEthernet0/0/0/0</name>
        </config>
      </interface>
      <interface>
        <name>GigabitEthernet0/0/0/1</name>
        <config>
          <name>GigabitEthernet0/0/0/1</name>
        </config>
      </interface>
      <interface>
        <name>GigabitEthernet0/0/0/2</name>
        <config>
          <name>GigabitEthernet0/0/0/2</name>
        </config>
      </interface>
    </interfaces>
  </lacp>
  <local-routes xmlns="http://openconfig.net/yang/local-routing">
    <static-routes>
      <static>
        <prefix>0.0.0.0/0</prefix>
        <config>
          <prefix>0.0.0.0/0</prefix>
        </config>
        <next-hops>
          <next-hop>
            <index>**10.0.0.1**</index>
            <config>
              <index>**10.0.0.1**</index>
              <next-hop>10.0.0.1</next-hop>
            </config>
          </next-hop>
        </next-hops>
      </static>
      <static>
        <prefix>192.168.1.2/32</prefix>
        <config>
          <prefix>192.168.1.2/32</prefix>
        </config>
        <next-hops>
          <next-hop>
            <index>**192.168.1.2**</index>
            <config>
              <index>**192.168.1.2**</index>
              <next-hop>192.168.1.2</next-hop>
            </config>
          </next-hop>
        </next-hops>
      </static>
    </static-routes>
  </local-routes>
  <bgp xmlns="http://openconfig.net/yang/bgp">
    <global>
      <config>
        <as>65501</as>
        <router-id>1.1.1.1</router-id>
      </config>
      <afi-safis>
        <afi-safi>
          <afi-safi-name xmlns:idx="http://openconfig.net/yang/bgp-types">idx:ipv4-unicast</afi-safi-name>
          <config>
            <afi-safi-name xmlns:idx="http://openconfig.net/yang/bgp-types">idx:ipv4-unicast</afi-safi-name>
            <enabled>true</enabled>
          </config>
        </afi-safi>
      </afi-safis>
    </global>
    <peer-groups>
      <peer-group>
        <peer-group-name>telefonica_test</peer-group-name>
        <config>
          <peer-group-name>telefonica_test</peer-group-name>
          <peer-as>65501</peer-as>
        </config>
        <timers>
          <config>
            <keepalive-interval>10</keepalive-interval>
            <hold-time>30</hold-time>
          </config>
        </timers>
        <transport>
          <config>
            <local-address>GigabitEthernet0/0/0/1</local-address>
          </config>
        </transport>
        <afi-safis>
          <afi-safi>
            <afi-safi-name xmlns:idx="http://openconfig.net/yang/bgp-types">idx:ipv4-unicast</afi-safi-name>
            <config>
              <afi-safi-name xmlns:idx="http://openconfig.net/yang/bgp-types">idx:ipv4-unicast</afi-safi-name>
              <enabled>true</enabled>
            </config>
          </afi-safi>
        </afi-safis>
      </peer-group>
    </peer-groups>
    <neighbors>
      <neighbor>
        <neighbor-address>192.168.1.2</neighbor-address>
        <config>
          <neighbor-address>192.168.1.2</neighbor-address>
          <peer-group>telefonica_test</peer-group>
        </config>
        <afi-safis>
          <afi-safi>
            <afi-safi-name xmlns:idx="http://openconfig.net/yang/bgp-types">idx:ipv4-unicast</afi-safi-name>
            <config>
              <afi-safi-name xmlns:idx="http://openconfig.net/yang/bgp-types">idx:ipv4-unicast</afi-safi-name>
              <enabled>true</enabled>
            </config>
          </afi-safi>
        </afi-safis>
      </neighbor>
    </neighbors>
  </bgp>
  <routing-policy xmlns="http://openconfig.net/yang/routing-policy">
    <policy-definitions>
      <policy-definition>
        <name>pass-all</name>
        <config>
          <name>pass-all</name>
        </config>
        <statements>
          <statement>
            <name>statement-2930648099</name>
            <config>
              <name>statement-2930648099</name>
            </config>
          </statement>
        </statements>
      </policy-definition>
    </policy-definitions>
  </routing-policy>
</data>
```