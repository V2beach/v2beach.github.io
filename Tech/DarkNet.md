![Darkweb.](/assets/Thumbnail_Darkweb.png)
```
Last login: Thu Nov  9 17:36:59 on ttys008
/Applications/Tor\ Browser.app/Contents/MacOS/firefox ; exit;
(base) v2beach@V2beachs-mbp-m1 ~ % /Applications/Tor\ Browser.app/Contents/MacOS/firefox ; exit;
2023-11-09 17:37:11.262 firefox[7898:112628] Failed to get font faces: <CFArray 0x10d133970 [0x1e547c000]>{type = mutable-small, count = 1, values = (
	0 : <CFURL 0x1027673a0 [0x1e547c000]>{string = file:///Applications/Tor%20Browser.app/Contents/Resources/fonts/000_README.txt, encoding = 134217984, base = (null)}
)}.
2023-11-09 17:37:11.447 plugin-container[7899:112694] nil host used in call to allowsSpecificHTTPSCertificateForHost
2023-11-09 17:37:11.447 plugin-container[7899:112694] nil host used in call to allowsAnyHTTPSCertificateForHost:
2023-11-09 17:37:11.449 plugin-container[7899:112694] nil host used in call to allowsSpecificHTTPSCertificateForHost
2023-11-09 17:37:11.449 plugin-container[7899:112694] nil host used in call to allowsAnyHTTPSCertificateForHost:
2023-11-09 17:37:11.450 plugin-container[7899:112699] nil host used in call to allowsSpecificHTTPSCertificateForHost
2023-11-09 17:37:11.450 plugin-container[7899:112699] nil host used in call to allowsAnyHTTPSCertificateForHost:
2023-11-09 17:37:11.874 plugin-container[7901:112790] Failed to get font faces: (
    "file:///Applications/Tor%20Browser.app/Contents/Resources/fonts/000_README.txt"
).
UNSUPPORTED (log once): POSSIBLE ISSUE: unit 1 GLD_TEXTURE_INDEX_2D is unloadable and bound to sampler type (Float) - using zero texture because texture unloadable
2023-11-09 17:37:12.220 plugin-container[7902:112850] Failed to get font faces: (
    "file:///Applications/Tor%20Browser.app/Contents/Resources/fonts/000_README.txt"
).
Exiting due to channel error.
Exiting due to channel error.
zsh: terminated  /Applications/Tor\ Browser.app/Contents/MacOS/firefox

Saving session...
...copying shared history...
...saving history...truncating history files...
...completed.

[Process completed]
```
试了一整个下午，tor本身可以连接但在brave里连接不上，tor browser始终报上面的错。

失败，之后换windows/freebsd再试。