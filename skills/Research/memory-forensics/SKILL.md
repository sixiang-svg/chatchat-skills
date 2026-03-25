---
id: memory-forensics
name: Memory Forensics
description: Master memory forensics techniques including acquisition, process analysis, and artifact extraction using Volatility.
category: Research
requires: []
examples:
  - How do I acquire a memory dump from a Windows machine using WinPmem?
  - Use Volatility to list all active processes from this memory.raw file.
---

# Memory Forensics

Comprehensive techniques for acquiring, analyzing, and extracting artifacts from memory dumps for incident response and malware analysis.

## Instruction
- Conduct live memory acquisition using tools like WinPmem (Windows) or LiME (Linux), ensuring data integrity and hash verification.
- Identify the correct operating system profile to enable accurate symbol mapping during analysis.
- Analyze active and hidden processes to detect suspicious activity, such as process hollowing or injection.
- Extract network artifacts including active connections, listening ports, and historical DNS queries.
- Recover forensic artifacts like registry hives, cached credentials, and command-line history.
- Use specialized plugins to scan for rootkits, malicious drivers, and obfuscated strings within memory sections.
- Correlate memory findings with disk and network forensics to build a comprehensive incident timeline.

## When to Use
- When performing incident response to identify malware residing only in volatile memory.
- When recovering ephemeral data such as encryption keys, unsaved documents, or private browser sessions.
- When analyzing sophisticated threats that utilize anti-forensic or fileless execution techniques.

## Output
- A detailed forensic report listing identified suspicious processes, network connections, and extracted artifacts.
- Extracted malware samples or suspicious memory dumps for further reverse engineering.
- A structured incident timeline based on memory-resident timestamps.
## Best Practices

### Acquisition Best Practices

1. **Minimize footprint**: Use lightweight acquisition tools
2. **Document everything**: Record time, tool, and hash of capture
3. **Verify integrity**: Hash memory dump immediately after capture
4. **Chain of custody**: Maintain proper forensic handling

### Analysis Best Practices

1. **Start broad**: Get overview before deep diving
2. **Cross-reference**: Use multiple plugins for same data
3. **Timeline correlation**: Correlate memory findings with disk/network
4. **Document findings**: Keep detailed notes and screenshots
5. **Validate results**: Verify findings through multiple methods

### Common Pitfalls

- **Stale data**: Memory is volatile, analyze promptly
- **Incomplete dumps**: Verify dump size matches expected RAM
- **Symbol issues**: Ensure correct symbol files for OS version
- **Smear**: Memory may change during acquisition
- **Encryption**: Some data may be encrypted in memory
