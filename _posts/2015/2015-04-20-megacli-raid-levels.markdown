---
layout: post
title: MegaCLI, Raid Levels
date: 2015-04-20 13:07:10.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_pending: '1'
  is_reblog: '1'
  post_id: '3'
  blog_id: '54028808'
  reblog_snapshot: "O:8:\"stdClass\":7:{s:5:\"title\";s:20:\"MegaCLI, Raid Levels\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2015-01-15
    01:17:29\";s:9:\"permalink\";s:63:\"https://globalroot.wordpress.com/2013/06/18/megacli-raid-levels\";s:7:\"content\";s:16775:\"<div
    class=\"reblogged-content\">\n\n<h3>Common invocations of MegaCLI</h3>\r\n<h1>Get
    an Overview of controllers and attached disk arrays</h1>\r\n<span style=\"color:#0000ff;\">./MegaCli64
    -AdpAllInfo -aALL (extracted info below)</span><i>\r\n<span style=\"color:#0000ff;\">./MegaCli64
    -CFGDsply -aALL </span> shows same info, with same verbosity</i>\r\n\r\nAdapter
    #0\r\n========================================\r\n<span style=\"color:#999999;\">Product
    Name    : PERC H800 Adapter</span><span style=\"color:#999999;\"> Serial No      
    : 25B0088</span>\r\n<pre><span style=\"color:#999999;\">Link Speed           :
    0</span>\r\n<span style=\"color:#999999;\"> Number of Frontend Port: 0</span>\r\n<span
    style=\"color:#999999;\"> Device Interface  : PCIE</span>\r\n<span style=\"color:#999999;\">Number
    of Backend Port: 8</span>\r\n<span style=\"color:#999999;\"> Port  :  Address</span>\r\n
    <span style=\"color:#999999;\">0        500c04f2e958eebf </span>\r\n <span style=\"color:#999999;\">1       
    500c04f2e958ee3f </span>\r\n <span style=\"color:#999999;\">2        0000000000000000
    </span>\r\n <span style=\"color:#999999;\">3        0000000000000000 </span>\r\n
    <span style=\"color:#999999;\">4        0000000000000000 </span>\r\n <span style=\"color:#999999;\">5       
    0000000000000000 </span>\r\n <span style=\"color:#999999;\">6        0000000000000000
    </span>\r\n <span style=\"color:#999999;\">7        0000000000000000</span>\r\nDevice
    Present\r\n ================\r\n <span style=\"color:#999999;\">Virtual Drives   
    : 1\r\n </span><span style=\"color:#999999;\">Degraded          : 0   </span>\r\n
    <span style=\"color:#999999;\">Offline               : 0 </span>\r\n <span style=\"color:#999999;\">Physical
    Devices  : 13\r\n </span><span style=\"color:#999999;\">Disks                :
    12   </span>\r\n <span style=\"color:#999999;\">Critical Disks     : 0   </span>\r\n
    <span style=\"color:#999999;\">Failed Disks      : 0</span></pre>\r\n(snip)\r\n\r\nAdapter
    #1\r\n==============================================================================\r\n<span
    style=\"color:#999999;\">Product Name    : PERC 6/i Integrated</span>\r\n<span
    style=\"color:#999999;\">Serial No       : 1122334455667788</span>\r\n<pre>Device
    Present\r\n ================\r\n <span style=\"color:#999999;\">Virtual Drives     
    : 1   </span>\r\n <span style=\"color:#999999;\">Degraded            : 0   </span>\r\n
    <span style=\"color:#999999;\">Offline                : 0 </span>\r\n <span style=\"color:#999999;\">Physical
    Devices  : 3   </span>\r\n <span style=\"color:#999999;\">Disks                
     : 2   </span>\r\n <span style=\"color:#999999;\">Critical Disks       : 0   </span>\r\n
    <span style=\"color:#999999;\">Failed Disks         : 0</span>\r\nSettings\r\n
    ================\r\n <span style=\"color:#999999;\">Current Time                    
    : 12:16:19 6/18, 2013</span>\r\n <span style=\"color:#999999;\">Predictive Fail
    Poll Interval    : 300sec</span>\r\n <span style=\"color:#999999;\">Rebuild Rate                    
    : 30%</span>\r\n <span style=\"color:#999999;\">Reconstruction Rate             
    : 30%</span>\r\n <span style=\"color:#999999;\">Cache Flush Interval            
    : 4s</span>\r\n <span style=\"color:#999999;\">Max Drives to Spinup at One Time
    : 2</span>\r\n <span style=\"color:#999999;\">Delay Among Spinup Groups       
    : 12s</span>\r\n <span style=\"color:#999999;\">Restore HotSpare on Insertion   
    : Disabled</span>\r\n <span style=\"color:#999999;\">Expose Enclosure Devices        
    : Disabled</span>\r\n <span style=\"color:#999999;\">Maintain PD Fail History        
    : Disabled</span>\r\n <span style=\"color:#999999;\">Maximum number of direct
    attached drives to spin up in 1 min : 0</span>\r\n <span style=\"color:#999999;\">Auto
    Enhanced Import             : No</span>\r\n\r\nCapabilities\r\n ================\r\n
    The last paragraph above mentions many unusual RAID levels. Here is a brief explanation
    of the more exotic.\r\n <span style=\"color:#999999;\">RAID Level Supported            
    : </span>\r\n <span style=\"color:#999999;\">    RAID0, RAID1, RAID5, RAID6, RAID00,
    RAID10, RAID50, RAID60, PRL 11, PRL 11 with spanning, </span>\r\n <span style=\"color:#999999;\">   
    SRL 3 supported, PRL11-RLQ0 DDF layout with no span, PRL11-RLQ0 DDF layout with
    span</span>\r\n <span style=\"color:#999999;\">Supported Drives                
    : SAS, SATA</span></pre>\r\n-- <span style=\"text-decoration:underline;\">Explanations
    of RAID Levels </span>\r\n\r\n<span style=\"color:#888888;\">This PDF explains
    secondary level raid etc: <span style=\"text-decoration:underline;\"> <a href=\"http://www.snia.org/sites/default/files/SNIA_DDF_Technical_Position_v2.0.pdf\"><span
    style=\"color:#888888;text-decoration:underline;\">http://www.snia.org/sites/default/files/SNIA_DDF_Technical_Position_v2.0.pdf</span></a></span>  
    </span>\r\n<ul>\n<li>\n<span style=\"text-decoration:underline;\">RAID6 - Dual
    Parity RAID</span>:\r\nStriped stripes: Break up a file into stripes and stripe
    it across all drives. Need multiple raid controllers and large files for this
    to provide benefit.</li>\r\n\t<li>\n<span style=\"text-decoration:underline;\">PRL11-RLQ0
    layout</span> : aka <span style=\"text-decoration:underline;\">RAID1E Integrated
    Adjacent Stripe Mirroring</span>\r\nEach block is written twice. The location
    of the mirror/parity block is defined is being in the same extent, but on the
    next adjacent disk. Spanning is needed when you have different sized Basic Virtual
    Drives (subdisks).</li>\r\n\t<li>\n<span style=\"text-decoration:underline;\">SRL3:
    Spanned Secondary Raid Level 3</span>:\r\n(less protection) : data stripes are
    allocated pretty much where ever they can be - striped or concatenated from any
    available subdisks (aka bvd). The subdisk may or may not be raid-protected.</li>\r\n\t<li>\n<span
    style=\"text-decoration:underline;\">RAID Level Qualifier:</span>\r\nThis little
    guy says nothing about the level of protection, only that there are several ways
    to \"skin a disk\". RLQ assigns numbers to them.</li>\r\n</ul>\n<h2></h2>\r\n<h2>Examine drives
    on one adapter</h2>\r\n<a href=\"mailto:root@auspcrpbak03:MegaCli\">root@auspcrpbak03:MegaCli</a>&gt;
    ./<span style=\"color:#0000ff;\">MegaCli64 -LdPdInfo -a0\r\n</span>\r\nNotes:
    There are 12 drives of about 1.8TB. We're running RAID6, so we expect to lose
    2 drives to parity and get 18TB.\r\n<pre><span style=\"text-decoration:underline;\">Adapter
    #0</span>\r\n<span style=\"color:#999999;\">Number of Virtual Disks: 1 </span>\r\n
    <span style=\"color:#999999;\">Virtual Drive: 0 (Target Id: 0) </span>\r\n <span
    style=\"color:#999999;\">Name                     :Virtual Disk 0 </span>\r\n
    <span style=\"color:#999999;\">RAID Level              : <span style=\"color:#ff9900;\">Primary-6,
    Secondary-0, RAID Level Qualifier-3</span> </span>\r\n <span style=\"color:#999999;\">Size                       
    : 18.188 TB                  ( <em><span style=\"color:#c0c0c0;\">This is size
    presented to OS </span></em>) </span>\r\n <span style=\"color:#999999;\">Sector
    Size              : 512 </span>\r\n <span style=\"color:#999999;\">Parity Size               :
    3.637 TB          (<em><span style=\"color:#c0c0c0;\">In addition to the 18T.
    For RAID6 we have two</span></em>)</span>\r\n <span style=\"color:#999999;\">State                      
    : Optimal </span>\r\n <span style=\"color:#999999;\">Number Of Drives     : 12
    </span>\r\n <span style=\"color:#999999;\">Current Cache Policy : WriteThrough,
    ReadAdaptive, Direct, No Write Cache if Bad BBU Number of PDs: 12</span></pre>\r\n---\r\n<span
    style=\"text-decoration:underline;\"><span style=\"color:#ff9900;text-decoration:underline;\">Explanation
    of Raid Levels: </span></span>\r\n['Primary-0, Secondary-0, RAID Level Qualifier-0']
    = RAID-0\r\n['Primary-1, Secondary-0, RAID Level Qualifier-0'] = RAID-1\r\n['Primary-5,
    Secondary-0, RAID Level Qualifier-3'] = RAID-5\r\n['Primary-6, Secondary-0, RAID
    Level Qualifier-3'] = RAID-6\r\n['Primary-1, Secondary-3, RAID Level Qualifier-0']
    = RAID-10\r\n\r\nSource: http://tools.rapidsoft.de/perc/rs_check_raid_perc5i.class.php.txt\r\n<pre>
    --- PD: 0 \r\n<span style=\"color:#999999;\">Information Enclosure Device ID:
    16 </span> \r\n<span style=\"color:#999999;\">Slot Number        : 0 </span> \r\n<span
    style=\"color:#999999;\">Drive's position    : DiskGroup: 0, Span: 0, Arm: 0 \r\n</span>
    <span style=\"color:#999999;\">Enclosure position: N/A </span> \r\n<span style=\"color:#999999;\">Device
    Id             : 13 </span> \r\n<span style=\"color:#999999;\">WWN: 5000C500558ADE08
    </span> \r\n<span style=\"color:#999999;\">Sequence Number: 2</span> \r\n<span
    style=\"color:#999999;\">Media Error Count : 0 </span> \r\n<span style=\"color:#999999;\">PD
    Type               : SAS</span>\r\n<span style=\"color:#999999;\">Raw Size: 1.819
    TB [0xe8e088b0 Sectors]       (<span style=\"color:#c0c0c0;\"><em>This is real
    1024M size, not 1000M. It's sold as a 2TB drive</em></span>)</span>\r\n <span
    style=\"color:#999999;\">Firmware state:    Online, Spun Up Device </span>\r\n
    <span style=\"color:#999999;\">SAS Address(0):   0x5000c500558ade09 </span>\r\n
    <span style=\"color:#999999;\">SAS Address(1):   0x5000c500558ade0a </span>\r\n
    <span style=\"color:#999999;\">Connected Port Number:   1(path0) 0(path1) </span>\r\n
    <span style=\"color:#999999;\">Inquiry Data:         SEAGATE ST32000645SS    RS0FZ1K0AV9E
    </span>\r\n <span style=\"color:#999999;\">Drive has flagged a S.M.A.R.T alert
    : No</span>\r\nPD: 1\r\n <span style=\"color:#999999;\">Information Enclosure
    Device ID: 16 </span>\r\n <span style=\"color:#999999;\">Slot Number:                              1
    </span>\r\n <span style=\"color:#999999;\">Drive's position:   DiskGroup: 0, Span:
    0, Arm: 1 Device Id: 12 </span>\r\n <span style=\"color:#999999;\">WWN:                                      
     5000C500558AEBA4 </span>\r\n <span style=\"color:#999999;\">Sequence Number:                    
    2 </span>\r\n <span style=\"color:#999999;\">Media Error Count: 0 PD Type:   
    SAS</span></pre>\r\n&lt; and much more &gt;\r\n<h2>Optional toppings for most
    LD configurations:</h2>\r\n<ul>\n<li>\n<span style=\"color:#33cccc;\">WT</span>
    :      WriteThrough   safer.  Only considered to be written once on disk.</li>\r\n\t<li>\n<span
    style=\"color:#33cccc;\">WB</span>:       WriteBack       faster. Data in disk
    cache is considered written</li>\r\n\t<li>\n<span style=\"color:#33cccc;\">NORA</span>
    :  No Read Ahead   vs</li>\r\n\t<li>\n<span style=\"color:#00ffff;\">RA</span>:
           ReadAhead   vs</li>\r\n\t<li>\n<span style=\"color:#00ffff;\">ADRA</span>
    :   Adaptive ReadAhead where if the previous two requests were sequential it pre-loads
    the next in sequence.</li>\r\n\t<li>\n<span style=\"color:#33cccc;\">Cached</span>:
     Cache reads.</li>\r\n\t<li>\n<span style=\"color:#33cccc;\">Direct</span>:  
     Only the previous read is cached.</li>\r\n\t<li>\n<span style=\"color:#00ffff;\">-strpsz<em>M</em></span>     
    : Stripe size      so -strpsz64 means 64kb stripe size.</li>\r\n\t<li>\n<span
    style=\"color:#00ffff;\">Hsp[E0:S0] </span>: Choose this drive to be a hot-spare</li>\r\n</ul>\n<h1>Dump
    the Event Log for the Adapter</h1>\r\n./<span style=\"color:#0000ff;\">MegaCli64
    -AdpEventLog -GetLatest 20 -f /tmp/events.txt -a0</span>\r\n<h2></h2>\r\n<h2>Build
    a Virtual Disk</h2>\r\n<span style=\"color:blue;\">MegaCli -CfgLdAdd -r</span><span
    style=\"color:#800080;\">X</span> <span style=\"color:blue;\">[<span style=\"color:#008000;\">E0:S0,E1:S1</span>,...]
    <span style=\"color:#33cccc;\">[WT|WB] [NORA|RA|ADRA] [Direct|Cached]</span>  
    [CachedBadBBU|NoCachedBadBBU] [-szXXX [-szYYY ...]]\r\n[-<span style=\"color:#33cccc;\">strpszM</span>] 
    [-Hsp[E0:S0,...]] [-AfterLdX] | [Secure]\r\n[-Default| -Automatic| -None| -Maximum|
    -MaximumWithoutCaching] [-<span style=\"color:#0000ff;\">Cache</span>] [-enblPI]
    [-Force]-aN </span>\r\n\r\n<strong><span style=\"color:#800080;\">rX</span></strong>
    : Raid Level X. You can see your options by looking at the raid adapter settings
    (top of this page).\r\nIn this example we can choose 0,1,5,6,00,10,50,60  and
    more\r\n\r\n<span style=\"color:#008000;\">[E0:S1,E0:S3]</span> - Enclosure0:Slot1,
    Enclosure0:Slot3 : 2 Drives to use in the VD. Include the square brackets.\r\n<h2></h2>\r\n<h2>Configure
    disks as JBOD</h2>\r\n<span style=\"color:#0000ff;\">MegaCli64 -CfgEachDskRAID0
    -a0</span>\r\n<h2>Configure RAID 10</h2>\r\n<span style=\"color:#0000ff;\">MegaCli64
    -CfgSpanAdd -R10 -Array0 [E0:S1,E0:S2,E0,S3] -Array1 [E1:S0,E1:S1,E1:S2] + Toppings
    above</span>\r\n<h2></h2>\r\n<h2>Delete the first logical drive on the first controller</h2>\r\n<span
    style=\"color:#0000ff;\">MegaCli64 -CfgLdDel -L0 -a0</span>\r\n<h2></h2>\r\n<h2>Replace
    a Failed Drive</h2>\r\n<span style=\"color:#0000ff;\">MegaCli64 -PDOffline -PhysDrv
    [32:4] -a0</span>\r\n<span style=\"color:#0000ff;\">MegaCli64 -PDPrpRmv -PhysDrv
    [32:4] -a0</span>\r\n<em>Pull the drive, insert a new one</em>\r\n<span style=\"color:#0000ff;\">MegaCli64
    -Pdgetmissing -a0</span>\r\n\r\n<address>Adapter 0 - Missing Physical drives\r\nNo.
    Array Row Size Expected\r\n0 1 4 1907200 MB</address>\n<span style=\"color:#0000ff;\">MegaCli64
    -PdReplaceMissing -PhysDrv [32:4] -Array1 -row4 -a0</span>\r\n<h2></h2>\r\n<h2>Rebuild
    the Array</h2>\r\n<span style=\"color:#0000ff;\">MegaCli64 -PDRbld -Start -PhysDrv
    [32:4] -a0</span>\r\n<h2></h2>\r\n<h2>Show Battery Backup Info</h2>\r\n<span style=\"color:#0000ff;\">MegaCli64
    -AdpBbuCmd -aALL</span>\r\n<h2></h2>\r\n<h2>RAID Rebuild Rate - Increase to 90
    Percent</h2>\r\nMegaCli64 -AdpSetProp BgiRate 90 -aALL\r\n<h2></h2>\r\n<h2>Save
    configuration to filesystem</h2>\r\n<span style=\"color:blue;\">MegaCli64 -CfgSave
    -fFilename -a0</span>\r\n\r\nWhen you replace controllers, you can duplicate the
    previous config. In BIOS look for 'Add Saved Configuration'. Say 'Y' to the warning
    to import it from the disks. (Be sure that your disk array is healthy first.)\r\n<h2>RAID
    10 and variants</h2>\r\nDue to Dawid's comment below, I did some more research,
    refreshed my recollections about RAID10 and similar configurations and have the
    following comments.\r\n<em>   <strong>RAID10</strong> is shorthand for<strong>
    RAID1+0</strong> which is a stripe across mirrors.  (Take RAID1/mirrored disks and
    adding RAID0).</em>\r\n<em>   <strong>RAID01</strong> is shorthand for <strong>RAID0+1</strong>
    which mirrors  disks that are striped. (Take RAID0 disks and add RAID1 to them).</em>\r\nRAID01
    is a less common config because RAID10 offers more redundancy (a big reason for
    why we RAID) and few disadvantages compared to RAID01.\r\nIn the case of four
    disks (which is a common config), I don't (personally) see a big difference, but
    things get interesting when you have six or more disks. So let's start there.\r\n\r\nAt
    this point, an analogy may make things more interesting, even if most readers
    already fully understand what I am saying. When I was younger, I played a game
    called Battleships.  Assuming you have to carry eight squares of cargo, which
    would you prefer: two four-unit battleships or four two-unit destroyers? When
    the bombs start falling, you would much prefer to have your cargo in four different
    locations. While this is true when a malevolent opponent is trying to take them
    out, it's also true when chaos sets in on your disk arrays. Forcing Murphy to
    take out both disks in the same mirror (for example both yellows from the left
    picture), rather than one disk from each stripe is a good play (one red and one
    blue from the right-most image). And it's more colorful in diagrams.\r\n<ul>Illustration
    of  RAID01 in a 2-by-4 config  versus  RAID10 in a 4-by-2 config</ul>\n<a href=\"http://globalroot.files.wordpress.com/2013/06/raidbattleships2.png\"><img
    class=\"alignnone size-large wp-image-83\" src=\"http://globalroot.files.wordpress.com/2013/06/raidbattleships1.png?w=529\"
    alt=\"RaidBattleships\" width=\"529\" height=\"333\"></a>\r\n\r\nIt also makes
    clearer the \"Primary\" and \"Secondary\" listings in the output from megacli.\r\nPrimary
    is the \"<span style=\"color:#ff6600;\">RAID1</span>\" part of  \"RAID1+0\".  It
    is the more basic/fundamental element of the array - a mirror.\r\nSecondary is
    how you organize the primal units you first created. For a RAID1+0, we stripe
    them (RAID 0).\r\n\r\nDawid's situation was that he has 4 disks, but they show
    as (Pri-1, Sec-0, Qual-0)  which is how megacli's represents a plain mirror. I
    suspect that he manually created the striped disks then mirrored them and that
    megacli did not keep track of all the steps. I expect that it will work out just
    fine, but it would be more obvious and faster if next time he ran 'megacli <span
    style=\"color:blue;\">-CfgLdAdd -r10 ...' </span>\n</div>\";}"
---

