---
layout: post
title: Securing your system with Snort
date: 2012-06-25 13:32:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '4626206835473214712'
---
<div dir="ltr" style="text-align:left;">
<div class="post">Introduction</p>
<p>Snort—what's in a name? In the case of <span class="IL_AD" id="IL_AD6">open source<span class="IL_AD_ICON"></span></span> <span class="IL_AD" id="IL_AD4">software<span class="IL_AD_ICON"></span></span>,  a powerful network-intrusion prevention and detection system. Snort was  written over a weekend in 1998 by Martin Roesch. Martin wanted to write  a cross-platform sniffer that used pcap, a software library for packet capturing, rather than making direct calls into the kernel for sniffing. Result: the de facto standard for <span class="IL_AD" id="IL_AD1">intrusion detection and prevention<span class="IL_AD_ICON"></span></span>. If you do not already have Snort installed on your system, you can download it from http://www.snort.org/dl/. This <span class="IL_AD" id="IL_AD9">article<span class="IL_AD_ICON"></span></span> discusses Snort 2.4.3.</p>
<p>Snort  works by utilizing a rule-based language that combines the benefits of  signature inspection, protocol inspection, and anomaly-based inspection.  You can configure Snort to run in a few different modes Sniffer mode,  Packet Logger mode, Network Intrusion Detection (NIDS) mode.<br />Sniffer mode</p>
<p>Sniffer mode simply reads the packets from <span class="IL_AD" id="IL_AD3">the network<span class="IL_AD_ICON"></span></span> and displays them in a <span class="IL_AD" id="IL_AD8">stream<span class="IL_AD_ICON"></span></span> on the screen. If you just want to <span class="IL_AD" id="IL_AD5">print out<span class="IL_AD_ICON"></span></span> the TCP/IP packet headers to the screen, run:</p>
<p>snort -v</p>
<p>This command shows the IP and TCP/UDP/ICMP headers. If you want to see the <span class="IL_AD" id="IL_AD10">application<span class="IL_AD_ICON"></span></span> data in transit as well as the headers, run:</p>
<p>snort -vd</p>
<p>If you want an even more descriptive display, showing the data link layer headers, run:</p>
<p>snort -vde</p>
<p>Example 1 shows output from "snort -vde".</p>
<p>11/13-20:08:02.807867 0:E0:81:2F:FE:2C -&gt; 0:0:C:7:AC:2 type:0x800 len:0x5EA<br />66.179.164.20:22 -&gt; 24.136.161.188:62456 TCP TTL:64 TOS:0x10 ID:27401 IpLen:20 DgmLen:1500 DF</p>
<p>***A**** Seq: 0x50692152  Ack: 0xDD1E2B42  Win: 0x2180  TcpLen: 20<br />AA A8 5A 92 A7 BF DF 32 7D BF F7 7B 1B 5C 35 47  ..Z....2}..{.\5G<br />D6 52 B3 E2 97 6D 68 41 A6 53 2B 89 92 8E 10 8D  .R...mhA.S+.....<br />1B E0 C9 87 A8 71 91 EA D0 F4 1C 6C B4 DC D7 C4  .....q.....l....</p>
<p>B5 22 84 40 E5 09 0F B5 E9 1F 4E AC 96 6C A5 9D  .".@......N..l..<br />D9 AF 38 88 5F 2B 4B 8D 32 FC 4C 37 AB DA E1 EA  ..8._+K.2.L7....<br />61 D9 23 22 FD DA 20 32 E7 6C 48 60 2C 55 CB 99  a.#".. 2.lH`,U..<br />74 3A F5 7D 30 77 75 58 6B AE 80 2F 48 A5 FD F4  t:.}0wuXk../H...</p>
<p>B5 C7 CA 9D 42 EA 9B BF B6 74 E5 19 8F EF F1 8A  ....B....t......<br />2D 7E D0 55 0A 92 3E 72 CF 5F 89 53 FC 85 2F 25  -~.U..&gt;r._.S../%<br />72 8F B4 DD 40 BF 33 46 82 6D 21 98 8E A7 A0 A5  r...@.3F.m!.....<br />2E 32 54 ED 41 D4 2F C4 B6 6E BE 55 C0 95 78 7C  .2T.A./..n.U..x|</p>
<p>35 CA 06 4D 59 32 68 C8 3D 77 7A 73 FA 6A 78 1C  5..MY2h.=wzs.jx.<br />90 C7 CD 48 6D AE 0E 74 39 A0 4C F4 4E AC 49 06  ...Hm..t9.L.N.I.<br />A2 3F F3 BB 24 B7 05 7C B3 00 70 2E 65 E1 ED 1A  .?..$..|..p.e...<br />96 4C 93 CB A6 F5 68 B5 83 F8 08 F1 5C F2 9F 32  .L....h.....\..2</p>
<p>E1 F7 47 CF 2D 0B 35 DA 6A B5 D0 6D 49 9D 61 63  ..G.-.5.j..mI.ac<br />75 F2 4B 18 1F 02 C6 E4 9A 23 95 FE 21 6B A4 3E  u.K......#..!k.&gt;<br />06 40 CB 23 34 68 8F A1 C7 3C 98 20 14 8F 20 63  .@.#4h...&lt;. .. c<br />F7 FB 37 2B CC B9 2F 97 ED 5B 92 8D 96 84 0C 08  ..7+../..[......</p>
<p>E5 D4 29 A1 DF 4D 5B 33 EE 68 D3 F1 29 54 DF 0C  ..)..M[3.h..)T..<br />F0 37 44 4A DF 2F 07 68 49 9B 09 0A C1 C7 EC 89  .7DJ./.hI.......<br />50 CA 40 D3 5B A5 27 69 12 7E 49 34 1A F8 26 9C  P.@.[.'i.~I4..&amp;.<br />44 A0 87 C7 BC CB 46 8A 33 25 94 F6 89 72 64 E0  D.....F.3%...rd.</p>
<p>F0 AB 16 DB 52 A1 BE AC 3C 8B D6 CC 22 C7 0F B4  ....R...&lt;...&quot;...<br />86 6B BF EE A8 7E 1F 74 C7 34 14 AF 7C 50 BC 7F  .k...~.t.4..|P..<br />42 0C B8 98 8C C3 EC D6 FC 51 CE 1F B3 7D A1 48  B........Q...}.H<br />1D 89 96 AB 79 AA E0 A5 B8 F5 39 7C 27 4C 25 D0  ....y.....9|'L%.</p>
<p>5A 0C 81 13 07 19 6E 81 1C 3C 9F E5 1A 6D BA 18  Z.....n..&lt;...m..<br />DC 35 51 90 A1 1D 8E 57 7A 0A 56 BB 09 CB 3D 81  .5Q....Wz.V...=.<br />8F C5 84 83 88 ED CD 89 DB 81 4D F6 C7 04 A9 71  ..........M....q<br />43 65 FB 05 A4 56 E4 91 21 B1 AB 44 85 D8 12 BA  Ce...V..!..D....</p>
<p>CD 65 AA BA 32 D1 B7 FA 84 0E 18 56 BF 2E A5 10  .e..2......V....<br />72 C8 89 B8 6A 3B 75 33 3F 5F E4 77 24 EF 0C 13  r...j;u3?_.w$...<br />A8 56 BB 68 E3 88 D8 AF 18 83 02 B9 B1 2A E8 83  .V.h.........*..<br />33 2C 72 B4 49 9C F8 F3 92 03 2A 34 FB 4B 88 D6  3,r.I.....*4.K..</p>
<p>A3 FC C2 3D 14 2D 40 4C 4F A6 26 9F 17 22 F9 F3  ...=.-@LO.&amp;.."..<br />EE 7E 3F 5D 5E DE B5 D3 55 D7 CE 9B A5 68 DB 81  .~?]^...U....h..<br />C9 B1 16 96 11 59 6C D7 19 22 F1 62 D3 24 EB E1  .....Yl..".b.$..</p>
<p>D1 51 9F 4E 6C B9 0F 7A 61 FE 4F 00 7E 88 9B EE  .Q.Nl..za.O.~...<br />3E 27 7E 18 07 D9 27 F2 90 17 AA 11 7A 48 C5 57  &gt;'~...'.....zH.W<br />81 62 77 B6 A1 DF 72 AF E0 43 46 12 91 F1 5C FA  .bw...r..CF...\.<br />86 DF 7D 45 CF FC 45 63 21 A0 F7 6D 16 79 9F 14  ..}E..Ec!..m.y..</p>
<p>91 92 09 FB 33 E0 89 93 EF 95 F4 35 F3 B4 32 30  ....3......5..20<br />9A 0C 97 EE CF 9B 5D 73 07 E9 DC 74 B8 ED 48 00  ......]s...t..H.<br />DF 00 0A 69 6B F3 88 30 73 ED 98 8E 7C C8 FC 2C  ...ik..0s...|..,<br />0E 0C 84 74 3F 7A B2 CA 93 2F 21 AF 4F 62 D7 61  ...t?z.../!.Ob.a</p>
<p>04 56 28 30 61 91 C2 78 2D 04 63 2A E0 86 9C 84  .V(0a..x-.c*....<br />72 36 49 6E B7 91 F4 43 C2 A2 4C 03 6C F4 5B 14  r6In...C..L.l.[.<br />99 A2 12 3C A0 E3 18 CD BA 11 DF 0F 03 E0 A7 34  ...&lt;...........4<br />F9 7A 22 EE 09 62 1C 7B 24 DA 73 A8 5D 41 92 77  .z"..b.{$.s.]A.w</p>
<p>4A D5 ED AE 36 5C DA 65 2D BF 11 5B 5D B3 B6 08  J...6\.e-..[]...<br />E0 7D 44 E1 C0 27 A0 14 48 BE 5C 7B 89 39 25 34  .}D..'..H.\{.9%4<br />08 6E D6 0C 47 72 1B 96 DF 06 7E 9D 39 FE 3D 5E  .n..Gr....~.9.=^<br />04 D9 4F 96 4A E1 C8 B9 D5 33 26 AC E7 13 A2 F6  ..O.J....3&amp;.....</p>
<p>F2 4C 0F 22 E5 89 45 32 7E 03 CF 3A 53 F0 0E A6  .L."..E2~..:S...<br />8C 01 D3 FB 5B 0A 44 BF 7A 81 78 81 D7 63 AA 5F  ....[.D.z.x..c._<br />23 B0 23 7A B0 5C 12 75 E5 80 CD 47 AE FF 83 AE  #.#z.\.u...G....<br />46 B0 E9 3B 76 44 09 43 31 22 94 FE 1E 36 F7 40  F..;vD.C1"...6.@</p>
<p>A7 20 A4 80 04 E1 23 25 B9 1E 63 A2 11 4C 12 57  . ....#%..c..L.W<br />16 AC E2 00 A1 4B C9 24 C1 60 7C 4C 5C 7A 7E F7  .....K.$.`|L\z~.<br />6D 99 03 26 58 B4 DB EF A7 CE BE 68 EA 5A 4C F2  m..&amp;X......h.ZL.<br />0F 07 7B 2E A2 7C A3 DD 71 0A AF 96 2A 47 9D D3  ..{..|..q...*G..</p>
<p>54 42 5B 38 03 4A 4C CB 65 BE A2 C3 6B ED DD EB  TB[8.JL.e...k...<br />F6 D0 37 9D 00 66 E1 CA 8A 89 A5 03 5E A2 62 66  ..7..f......^.bf<br />07 EB F4 21 88 19 8C 06 44 E5 34 9D 9B 3D 6B 6E  ...!....D.4..=kn<br />CA 84 97 98 79 C1 EF 6A E9 7B 26 5B 03 73 61 6F  ....y..j.{&amp;[.sao</p>
<p>68 D1 03 E3 D6 D9 71 4E 08 BE 16 CE 6A 27 6E BE  h.....qN....j'n.<br />4F 5E E4 28 61 D9 55 FA 67 26 90 C5 52 76 D6 2D  O^.(a.U.g&amp;..Rv.-<br />9E 6E F5 C7 0C 87 A2 7B BA 4A 26 0C FB 4F 65 1A  .n.....{.J&amp;..Oe.<br />70 2F 44 98 8C 24 B6 91 60 91 39 FB D0 B7 7A E9  p/D..$..`.9...z.</p>
<p>24 0D D5 51 14 49 7D 0F 11 39 94 87 5D C8 7F 63  $..Q.I}..9..]..c<br />7C 8D C0 C8 6E C1 C5 D5 CD 39 9F 61 4A 76 9A 07  |...n....9.aJv..<br />9D 7B 03 2B 80 4F 30 48 F1 F1 AF 2F AB 9B CC 88  .{.+.O0H.../....<br />8D 51 3B A6 A0 C3 99 77 BF 56 86 36 3F 9E D9 94  .Q;....w.V.6?...</p>
<p>67 17 9C B7 3E C0 B0 16 85 21 61 78 BE 2B 4C DC  g...&gt;....!ax.+L.<br />71 A2 9A C9 8D 2F 60 D5 EA CD E1 D8 05 8D FA 4F  q..../`........O<br />D1 33 54 88 D1 73 47 AA 65 F2 30 DD 61 01 82 DC  .3T..sG.e.0.a...<br />2E 17 62 5D 87 F2 D7 88 4D E8 CD 50 BB 67 67 E3  ..b]....M..P.gg.</p>
<p>D7 D0 96 89 A2 9C 7F AB 56 F6 BF FD 88 CA 0B 95  ........V.......<br />3C B9 85 65 7C 0F D9 89 76 8F 74 F6 DE 1A 7B 99  &lt;..e|...v.t...{.<br />06 4F 18 AF DC DE 18 D0 75 FD 80 AD 0E 8B 9A D0  .O......u.......<br />DD F6 A7 E3 55 95 E8 FB 5A A9 AE 17 D7 0D DA B2  ....U...Z.......</p>
<p>FF 1D B0 0A AD 38 6C C0 1B BB 50 2E 85 49 F3 20  .....8l...P..I.<br />21 C2 A8 17 EF 70 1D EA EC E4 99 C0 DC 6F A5 96  !....p.......o..<br />DC D9 FD 90 73 FF 22 03 F0 C1 7E 2F 75 5F 6F 36  ....s."...~/u_o6<br />A5 8E 1C FE C1 CB B1 CC D4 C6 2C 0E FA 51 15 43  ..........,..Q.C</p>
<p>B0 70 2F E9 E5 A2 23 75 63 D8 2C D5 2B AD 36 EB  .p/...#uc.,.+.6.<br />8A 52 7D EE FA C0 15 F5 1B 21 9C 18 D0 76 06 52  .R}......!...v.R<br />FC 48 E2 D2 4F FD 0E 7C 85 C8 A4 C2 8E 7A 5A 27  .H..O..|.....zZ'<br />37 D8 4C E5 1A E6 94 9B A6 30 A3 BB 9C EC 59 ED  7.L......0....Y.</p>
<p>F6 94 49 51 46 1B D8 CE 98 F2 D1 0A 2F C2 07 3C  ..IQF......./..&lt;<br />87 58 FC EB                                      .X..</p>
<p>=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+=+</p>
<p>Example 1. Output from "snort -vde"</p>
<p>Of <span class="IL_AD" id="IL_AD2">course<span class="IL_AD_ICON"></span></span>, these switches can run in any combination, for example: "snort -vde", "snort -d -ev", and "snort -e -v -d".</p>
<p>Note:<br />     Snort will run as long as you let it, capturing information all the  while. To end the capture, press Ctrl-C. You will notice that when you  press Ctrl-C, you are presented with a summary of the information just  captured. Example 2 shows what this summary looks like after running  Snort for about a minute. </p>
<p>===============================================================================</p>
<p>Snort received 74260 packets<br />    Analyzed: 5923(7.976%)<br />    Dropped: 68337(92.024%)<br />===============================================================================</p>
<p>Breakdown by protocol:<br />    TCP: 1602       (2.157%)<br />    UDP: 4142       (5.578%)<br />   ICMP: 0          (0.000%)<br />    ARP: 6          (0.008%)<br />  EAPOL: 0          (0.000%)<br />   IPv6: 0          (0.000%)<br />ETHLOOP: 0          (0.000%)</p>
<p>    IPX: 0          (0.000%)<br />   FRAG: 0          (0.000%)<br />  OTHER: 1          (0.001%)<br />DISCARD: 0          (0.000%)<br />===============================================================================<br />Action Stats:</p>
<p>ALERTS: 0<br />LOGGED: 0<br />PASSED: 0<br />===============================================================================<br />Snort exiting</p>
<p>Example 2. Snort summary<br />Packet Logger mode</p>
<p>Packet  Logger mode enables you to log the contiguous stream of information to  disk. This is helpful when conducting analysis for a specified time  period or surrounding a modification in security policy or  configuration.</p>
<p>You will need to create and specify a logging directory, and Snort will automatically go into packet-logger mode.</p>
<p>Create a subdirectory called Piglet and run:</p>
<p>snort -dev -l ./Piglet</p>
<p>Example 3. Running Snort in Packet Logger mode</p>
<p>You  will see the stream of packet information go by, but it will also be  logged in tcpdump capture file format in the directory Piglet. In order  to read back from that log file, simply run the command in Example 4.  You will see the same stream of information that just flew by. If you do  not specify an output directory for the program, it will default to  /var/log/snort.</p>
<p>snort -r ./Piglet/logfile</p>
<p>Example 4. Reading the Snort logfile<br />Network Intrusion Detection (NIDS) mode</p>
<p>The  third Snort mode is Network Intrusion Detection (NIDS) mode. You may  not want to record every single packet that comes over the network, so  you can specify that Snort looks only on your local network. See Example  5.</p>
<p>./snort -dev -l ./log -h 192.168.0.0/24 </p>
<p>Example 5. Network Intrusion Detection (NIDS) mode</p>
<p>Common  use of NIDS mode employs a Snort configuration file, for example  "snort... -c snort.conf," where snort.conf is the name of your rules  file. This will apply the rules configured in the snort.conf file to  each packet to decide if an action based upon the rule type in the file  should be taken. The default snort.conf references several other rules  files, so read through the entire snort.conf before calling it from the  command line.</p>
<p>If you are going to use Snort over a long period as  an IDS, omit the -v switch from the command line for the sake of speed.  You can write information more quickly if you do not write verbosely to  the screen.</p>
<p>It is also not necessary to record the data-link  headers for most applications, so you can usually omit the -e switch,  too. See Example 6, "A typical Snort command".</p>
<p>./snort -d -h 192.168.1.0/24 -l ./log -c snort.conf</p>
<p>Example 6. A typical Snort command</p>
<p>Although  it is outside the scope of what Martin Roesch intended to do when he  wrote Snort, Snort 2.3.0 RC1 integrated the intrusion prevention system  (IPS) capability of snort_inline into the official Snort project.  Snort_inline gets packets from iptables instead of libpcap and then uses  new rule types to help iptables pass or drop packets based on Snort  rules. This is referred to as Inline Mode.</p>
<p>In order for  snort_inline to work properly, you have to compile the iptables code to  include "make install-devel" or have the libipq library installed. This  allows snort_inline to talk to iptables. You also need LibNet, which is  available from http://www.packetfactory.net.</p>
<p>You can use three  rule types when running Snort with snort_inline: drop, reject, and  sdrop. See the iptables documentation for more information.</p>
<p>What  does that mean to system security? How do I use Snort to secure my  system? The real power of Snort lies in the rules you set up for  monitoring. Some rule types are more useful than others depending on the  exposure your network receives. For example, a commonly used rule type  is payload detection based on content. A rule might look like Example 7,  "A Snort monitoring rule".</p>
<p>content: [!] "content_string";</p>
<p>Example 7. A Snort monitoring rule</p>
<p>Non-payload  detection rules are also available. For example, Example 8, "A  non-payload detection rule" shows a rule that checks against the IP  protocol header, in this case icmp.</p>
<p>alert ip any any -&gt; any any (ip_proto:icmp;)</p>
<p>Example 8. A non-payload detection rule</p>
<p>The  key to writing good rules is in keeping them streamlined. Poorly  written rules can cause Snort to duplicate checks or waste time finding  information it already has. Close analysis of the protocol in use can  turn up signature events. For example, a user logging into an ftp server  may pass the string "user root". A rule can be written to look for that  specific string on FTP's port. See Example 9, "A rule to detect a  particular string".</p>
<p>alert tcp any any -&gt; any any 21 (content:"user root"<img alt="Wink" border="0" src="{{ site.baseurl }}/assets/wink.gif" /></p>
<p>Example 9. A rule to detect a particular string</p>
<p>There  are as many ways to secure your system as rules you can think of. Snort  affords great flexibility in a powerful and open source solution.  Snort's popularity is due in part to its community of support beyond the  development of Snort. For more information, go to http://www.snort.org,  or refer to the recommended reading.<br />Further reading</p>
<p>    * Snort Cookbook by Angela D. Orebaugh, Simon Biles, Jacob Babbin; first edition March 2005<br />     * Nessus, Snort, &amp; Ethereal Power Tools: Customizing Open Source  Security Applications by Brian Caswell, Gilbert Ramirez, CISSP, Jay  Beale, Noam Rathaus. Publisher: Syngress, September 2005  </div>
</div>
