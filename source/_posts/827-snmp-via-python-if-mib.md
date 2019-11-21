---
title: 'snmp via python [IF-MIB]'
tags:
  - python
  - snmp
  - 运维
url: 827.html
id: 827
categories:
  - Python
date: 2014-11-24 16:43:05
---

依赖 pysnmp pysnmp-mibs \[python\] # -*- coding: utf-8 -*- ''' Created on 14/11/20. @author: seven ''' from pysnmp.entity.rfc3413.oneliner import cmdgen cmdGen = cmdgen.CommandGenerator() errorIndication, errorStatus, errorIndex, varBindTable = cmdGen.nextCmd( cmdgen.CommunityData('community_str'), cmdgen.UdpTransportTarget(('211.xx.169.xx', 161)), cmdgen.MibVariable('IF-MIB', 'ifNumber'), cmdgen.MibVariable('IF-MIB', 'ifDescr'), cmdgen.MibVariable('IF-MIB', 'ifType'), cmdgen.MibVariable('IF-MIB', 'ifMtu'), cmdgen.MibVariable('IF-MIB', 'ifSpeed'), cmdgen.MibVariable('IF-MIB', 'ifPhysAddress'), lookupValues=True ) if errorIndication: print(errorIndication) else: if errorStatus: print('%s at %s' % ( errorStatus.prettyPrint(), errorIndex and varBindTable\[-1\]\[int(errorIndex) - 1\] or '?' ) ) else: for varBindTableRow in varBindTable: for name, val in varBindTableRow: print('%s = %s' % (name.prettyPrint(), val.prettyPrint())) \[/python\]