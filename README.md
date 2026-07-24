# README
这里是我常用的自动化 rayder workflow ，建议在 debian、ubuntu、arch，mac …等拥有一定 unix 支持的系统上运行，enjoy ～

## attention

- gf rename gff
- gau rename gauu
- urlfinder-x rename urlfinder

## tools

```bash
recon: gau, katana, hakrawler, cariddi, urlfinder
portscan: naabu
domain: subfinder, rapiddns(https://github.com/nullt3r/rapiddns.git), puredns
vulnscan: nuclei, dddd
sup: httpx, anew, uro, gf, parallel, jq, morefind

# 不需要安装的第三方平台，在 workflow 中为被动收集 (passive)，此处提取 curl 命令，方便后续维护
curl -s -A "Mozilla/5.0" "https://crt.sh/?q=%.hfrea.org.cn&output=json"' | jq -r '.[].name_value'

curl -s -A "Mozilla/5.0" "https://api.certspotter.com/v1/issuances?domain=hfrea.org.cn&include_subdomains=true&expand=dns_names"' | jq -r '.[].dns_names' | morefind -d

curl -s -A "Mozilla/5.0" "http://web.archive.org/cdx/search/cdx?url=*.hfrea.org.cn/*&output=text&fl=original&collapse=urlkey"' | sed -e 's_https*://__' -e "s/\/.*//" | sort -u | anew web_archive_output.txt

curl -s -A "Mozilla/5.0" "https://jldc.me/anubis/subdomains/hfrea.org.cn"' | morefind -d

rapiddns -s hfrea.org.cn
```

## rely 

template & gf-patterns & wordlist - 保存在 `~`  目录下，方便后续调用

```bash
git clone https://github.com/Tripse/nuclei-tripse.git
git clone https://github.com/Tripse/gf-patterns-ng.git
git clone https://github.com/Tripse/wordlists.git
```

## install

> default system and env: linux-amd64

部署上，保留手工操作 & go install

```bash
# exclude tools: urlfinder, rapiddns, dddd
apt install go parallel jq -y
pipx install uro
go install github.com/lc/gau/v2/cmd/gau@latest
CGO_ENABLED=1 go install github.com/projectdiscovery/katana/cmd/katana@latest
go install github.com/hakluke/hakrawler@latest
go install -v github.com/edoardottt/cariddi/cmd/cariddi@latest
go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
go install -v github.com/tomnomnom/anew@latest
go install  github.com/mstxq17/MoreFind@latest
```

### recon

#### gau

```bash
  wget https://github.com/lc/gau/releases/download/v2.2.4/gau_2.2.4_linux_amd64.tar.gz
```

#### katana

```bash
wget https://github.com/projectdiscovery/katana/releases/download/v1.6.1/katana_1.6.1_linux_amd64.zip
```

#### hakrawler

```bash
go install github.com/hakluke/hakrawler@latest
```

#### cariddi

```bash
wget https://github.com/edoardottt/cariddi/releases/download/v1.4.6/cariddi_1.4.6_linux_amd64.zip
```

#### urlfinder

```bash
wget https://github.com/N-Next/URLFinder-x/releases/download/2025%2F1%2F17/URLFinder-x-linux-amd64
```

### portscan

naabu

```bash
wget https://github.com/projectdiscovery/naabu/releases/download/v2.6.1/naabu_2.6.1_linux_amd64.zip
```

### domain

#### subfinder

```bash
wget https://github.com/projectdiscovery/subfinder/releases/download/v2.14.0/subfinder_2.14.0_linux_amd64.zip
```

#### rapiddns

```bahs
git clone https://github.com/nullt3r/rapiddns.git
```

### vulnscan

#### nuclei

```bash
wget https://github.com/projectdiscovery/nuclei/releases/download/v3.8.0/nuclei_3.8.0_linux_amd64.zip
```

#### dddd

0.0

```bash
wget https://github.com/SleepingBag945/dddd/releases/download/v2.0.1/dddd_linux64
```

### sup

#### httpx

```bash
wget https://github.com/projectdiscovery/httpx/releases/download/v1.9.0/httpx_1.9.0_linux_amd64.zip
```

#### anew

```bash
wget https://github.com/tomnomnom/anew/releases/download/v0.1.1/anew-linux-amd64-0.1.1.tgz
```

#### uro

```bash
pipx install uro
```

#### morefind

```bash
wget https://github.com/mstxq17/MoreFind/releases/download/v1.5.7/MoreFind_v1.5.7_linux_x86_64.zip
```

#### parallel & jq

```bahs
apt install parallel jq
```

