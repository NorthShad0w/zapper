<H1 align="center">Privacy for your command line options</H2>
<H3 align="center">A Linux tool to hide from `ps`</H2>

Download (static and upx obfuscated binary):
```sh
curl -fL -o zapper https://da.gd/thczap/zapper-linux-x86_64 && \
chmod 755 zapper && \
./zapper -h
```

Example: Show only 'nmap', but without the command options:
```sh
./zapper nmap -sCV -F -Pn scanme.nmap.org
              ^^^^^^^^^^^^^^^^^^^^ will not show
```

Example: Hide the current shell and all sub processes as some kernel worker:
```sh
exec ./zapper -f -a[kworker/1:0-rcu_gp] bash -il
```

---
1. Does not require *root*
2. Works also on static binaries (e.g. GoLang)
3. Zaps the environment (*/proc/&lt;PID&gt;/environ*) as well
1. Does not rely on *LD_PRELOAD=*
5. Only 00.1% overhead.
6. Stops root from sniffing your processes (`-f`) (with strace).

---
Compile:
```sh
git clone https://github.com/hackerschoice/zapper.git
cd zapper
make
```

Exmaples
```sh
# Will show as 'ssh' without 'root@server'.
./zapper ssh root@server
```

```sh
# Will show as 'harmless' without '-sCV -F -Pn scanme...'
./zapper -a harmless nmap -sCV -F -Pn scanme.nmap.org
```

```sh
# Current shell and all child processes show as 'sh' without any options.
exec ./zapper -f -a THCwasHERE ${SHELL:-bash} -il
```

![Screenshot 2023-09-08 at 09 51 25](https://github.com/hackerschoice/zapper/assets/5938498/a8c8ceaa-456e-49d5-8dd9-fa09c6ff0060)

