# Spigot Log4J Patch
Mojang was logging the commant chat message as "format" not an "argument" to be replaced by the "format". Which allowed the advisory an access to the `JdniLookup` to initiate the remote code injection attack. 

Exploiting the JDNI Reference attack has been known before. But, the `MinecraftServer#sendMessage` allowed the attacker an access to the format string
which lead to the access to the JDNI lookup in which the attacker was able to apply the exploit on the Minecraft server and client.

EDIT: The attack doesn't need an access to the format. They just need their input to be logged.

## The Fix
~~This repository contains a patch that basically moves the command chat message to be an argument instead of being "format" in the
log4j logging method. Which is basically one line change that could've prevented this vulnerability completely.~~

EDIT: It won't fix it. Lookup for some reason works on the whole log message not on the "format" part. The patch includes the upgrade to `2.17`.

## References
- [CVE-2021-44228](https://github.com/advisories/GHSA-jfh8-c2jp-5v3q)
- [Dynamic Code Evaluation: JDNI Reference Injection](https://vulncat.fortify.com/en/detail?id=desc.dataflow.java.dynamic_code_evaluation_jndi_reference_injection)

