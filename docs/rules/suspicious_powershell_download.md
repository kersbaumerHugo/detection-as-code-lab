---
title: Suspicious PowerShell Remote Download
id: 8b22aec9-8644-4ef8-81c9-bfb3403f0276
status: experimental
description: Detect PowerShell command commonly used to download remote content.
author: Hugo Kersbaumer
date: 2026-06-30
tags:
  - attack.execution
  - attack.t1059.001
logsource:
  product: windows
  category: process_creation
detection:
  selection_img:
    Image|endswith:
      - '\powershell.exe'
      - '\pwsh.exe'
  selection_cmd:
    CommandLine|contains:
      - 'Invoke-WebRequest'
      - 'iwr '
      - 'DownloadString'
      - 'Net.WebClient'
      - 'curl '
      - 'wget '
  condition: selection_img and selection_cmd
falsepositives:
  - Legitimate administrative scripts
  - Software deployment automation
  - Internal IT troubleshooting
level: high
