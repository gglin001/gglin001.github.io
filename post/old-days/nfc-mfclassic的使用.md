## 0x01 help doc
```
allen@allen_ubuntu:~$ nfc-mfclassic --help
Usage: nfc-mfclassic f|r|R|w|W a|b u|U<01ab23cd> <dump.mfd> [<keys.mfd> [f]]
  f|r|R|w|W     - Perform format (f) or read from (r) or unlocked read from (R) or write to (w) or unlocked write to (W) card
                  *** format will reset all keys to FFFFFFFFFFFF and all data to 00 and all ACLs to default
                  *** unlocked read does not require authentication and will reveal A and B keys
                  *** note that unlocked write will attempt to overwrite block 0 including UID
                  *** unlocking only works with special Mifare 1K cards (Chinese clones)
  a|A|b|B       - Use A or B keys for action; Halt on errors (a|b) or tolerate errors (A|B)
  u|U           - Use any (u) uid or supply a uid specifically as U01ab23cd.
  <dump.mfd>    - MiFare Dump (MFD) used to write (card to MFD) or (MFD to card)
  <keys.mfd>    - MiFare Dump (MFD) that contain the keys (optional)
  f             - Force using the keyfile even if UID does not match (optional)
Examples: 

  Read card to file, using key A:

    nfc-mfclassic r a u mycard.mfd

  Write file to blank card, using key A:

    nfc-mfclassic w a u mycard.mfd

  Write new data and/or keys to previously written card, using key A:

    nfc-mfclassic w a u newdata.mfd mycard.mfd

  Format/wipe card (note two passes required to ensure writes for all ACL cases):

    nfc-mfclassic f A u dummy.mfd keyfile.mfd f
    nfc-mfclassic f B u dummy.mfd keyfile.mfd f

  Read card to file, using key A and uid 0x01 0xab 0x23 0xcd:

    nfc-mfclassic r a U01ab23cd mycard.mfd
```
## 0x02 trouble
总是对这几个选项不明白，之前有一次写入时使用命令：
```
nfc-mfclassic W a newdata.mfd mycard.mfd
```
注意：W大写。
因为该卡不是白卡，这样把卡给写坏了。。还没找到修复的办法。
命令：
```
nfc-mfclassic f A u dummy.mfd keyfile.mfd f
```
也无法挽救。
## 0x03 Right Way
Use 
```
nfc-mfclassic w a u newdata.mfd mycard.mfd
```
attention:w is down
这样就有以下流程：
1. mfoc读取密码
2. edit
3. 用edit后的file覆盖旧卡，注意使用上面的命令（加上u）
4. OK









