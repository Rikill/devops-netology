1. git show aefea
```
commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:29:58 2020 -0400

    Update CHANGELOG.md

```
2. git show-ref --tags -d | grep '85024d3'
```
85024d3100126de36331c6982bfaac02cdab9e76 refs/tags/v0.12.23^{}
```

3. git rev-parse $b8d720^@ 
```
^f83c8e1d18dd2cd4ad3b6f1424d861a5542fc4b8
```

4. git log --oneline v0.12.23..v0.12.24 
```
33ff1c03b (tag: v0.12.24) v0.12.24
b14b74c49 [Website] vmc provider links
3f235065b Update CHANGELOG.md
6ae64e247 registry: Fix panic when server is unreachable
5c619ca1b website: Remove links to the getting started guide's old location
06275647e Update CHANGELOG.md
d5f9411f5 command: Fix bug when using terraform login on Windows
4b6d06cc5 Update CHANGELOG.md
dd01a3507 Update CHANGELOG.md
225466bc3 Cleanup after v0.12.23 release
```

5. git log -S 'func providerSource' --pretty=format:'%H %N %ae %an %ad' 

```'
5af1e6234ab6da412fb8637393c5a17a1b293663  mart@degeneration.co.uk Martin Atkins Tue Apr 21 16:28:59 2020 -0700
8c928e83589d90a031f811fae52a81be7153e82f  mart@degeneration.co.uk Martin Atkins Thu Apr 2 18:04:39 2020 -0700
```

6. git log -S 'globalPluginDirs' --pretty=format:'%H %N %ae %an %ad'
```
125eb51dc40b049b38bf2ed11c32c6f594c8ef96  alisdair@users.noreply.github.com Alisdair McDiarmid Thu May 5 10:12:00 2022 -0400
22c121df8631c4499d070329c9aa7f5b291494e1  3526523+annawinkler@users.noreply.github.com Anna Winkler Tue May 3 12:28:41 2022 -0600
35a058fb3ddfae9cfee0b3893822c9a95b920f4c  mart@degeneration.co.uk Martin Atkins Thu Oct 19 17:40:20 2017 -0700
c0b17610965450a89598da491ce9b6b5cbd6393f  j.bardin@gmail.com James Bardin Mon Jun 12 15:04:40 2017 -0400
8364383c359a6b738a436d1b7745ccdce178df47  mart@degeneration.co.uk Martin Atkins Thu Apr 13 18:05:58 2017 -0700
```

7. git log -S 'synchronizedWriters' --pretty=format:'%H %N %ae %an %ad'

Самый первый коммит:  mart@degeneration.co.uk Martin Atkins Wed May 3 16:25:41 2017

```
bdfea50cc85161dea41be0fe3381fd98731ff786  j.bardin@gmail.com James Bardin Mon Nov 30 18:02:04 2020 -0500
fd4f7eb0b935e5a838810564fd549afe710ae19a  j.bardin@gmail.com James Bardin Wed Oct 21 13:06:23 2020 -0400
5ac311e2a91e381e2f52234668b49ba670aa0fe5  mart@degeneration.co.uk Martin Atkins Wed May 3 16:25:41 2017 -0700
```