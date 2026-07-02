---
title: Suspicious Long DNS Query
id: f2c4f8d3-5a76-446a-95e6-9e6c2f6d0103
status: experimental
description: 'Detects unusually long DNS queries that may
indicate tunneling or encoded data in subdomains.'
author: Hugo Kersbaumer
date: 2026-06-30
tags:
  - attack.command-and-control
  - attack.t1071.004
logsource:
  category: dns
detection:
  selection:
    query|re: '([a-zA-Z0-9]{40,}\.)+[a-zA-Z]{2,}'
  condition: selection
falsepositives:
  - Content delivery networks
  - Tracking domains
  - Cloud telemetry
  - Security tools performing DNS tests
level: medium
