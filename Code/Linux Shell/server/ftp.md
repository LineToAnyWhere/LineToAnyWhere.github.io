# Vsftp #
> # Vsftp简介 #

FTP(File transfer protocol)是一个文件传输协议，主要用于在服务器与客户端之间传输数据，该协议使用明文传送，适用于安全性、保密性较低的场景使用。以下是FTP的几个主要功能：
* ** 不同等级的用户身份：user,guest,anonymous **  
  FTP服务器默认有三种登录方式1.实体帐号，2.访客，3.匿名用户，三种登录方式所拥有的权限不同，能够使用的命令也不同。
* ** 日志记录 **  
  FTP可以使用syslogd来进行日志记录，包括用户的执行过的命令，传输过的数据等。可以在/var/log/里查看
* ** 限制用户目录（chroot） **  
  FTP为了防止用户随意浏览、更改其他目录数据，因此加入了chroot，将用户限制在自己的家目录中。

> # Vsftp关键概念 #

## 联机方式 ##
首先，要使用FTP进行数据传输通常需要建立两个连接，一个是**命令连接**，一个是**数据连接**，命令连接用于在客户端与服务端直接传输命令，即在客户端下达的各种命令（open，mkdir,ls,get,put等命令）由命令连接完成传输。数据连接用于在客户端与服务端直接产生数据上传、下载等事件时，完成具体需要的数据的传输。  
在建立数据连接时，又分为主动连接和被动连接，要说明的一点是，无论主动连接还是被动连接，都是相对于服务端来说的，即在主动给连接方式下，数据传输连接是由服务端主动向客户端连接，而在被动连接方式下，数据传输是由服务端被动得等待连接的到来。(命令连接的建立永远是客户端主动去连服务器啦，想都不用想的)

#### 主动连接 ####
* 客户端使用随机端口连接服务端21端口，完成命令连接的建立
* 客户端监听随机端口，并通过命令连接告知服务端
* 服务端使用20端口，主动连接客户端所告知的随机端口，完成数据连接的建立

#### 被动连接 ####
* 客户端使用随机端口连接服务端21端口，完成命令连接的建立
* 服务端监听随机端口，并通过命令连接告知客户端
* 客户端使用随机端口，连接服务端端所告知的随机端口，完成数据连接的建立

> # Vsftp安装 #

vsftp的安装非常简单，以CentOS为例，只要执行`yum install -y vsftpd`即可;Ubuntu执行`apt-get install vsftpd`即可。其他版本的安装网上有很多教程，不一一举例。
> # Vsftp配置 #

## vsftpd.conf ##
**所有配置文件中等号两边都不能有空格**  
该文档为vsftpd的主要配置文件，它的实际目录为`/etc/vsftpd/vsftpd.conf`
```
ssl_enable 默认值：NO
如果启用，并且vsftpd是针对OpenSSL编译的，vsftpd将通过SSL支持安全连接。这适用于控制连接（包括登录）以及数据连接。同时还需要一个支持SSL的客户端。vsftpd不能保证OpenSSL库的安全性。通过启用此选项，将默认您信任安装的OpenSSL库的安全性。

allow_anon_ssl 默认值：NO
仅适用于 ssl_enable 开启。如果设置为YES，匿名用户将被允许使用安全的SSL连接。


anon_mkdir_write_enable
如果设置为YES，匿名用户将被允许在特定条件下创建新目录。为了使其工作， 必须激活选项 write_enable，并且匿名ftp用户必须对父目录具有写入权限。
默认值：NO

anon_other_write_enable
如果设置为YES，匿名用户将被允许执行除上载和创建目录之外的写操作，例如删除和重命名。这通常不推荐，但包括为完整性。
默认值：NO

anon_upload_enable
如果设置为YES，匿名用户将被允许在特定条件下上传文件。为了使其工作， 必须激活选项 write_enable，匿名ftp用户必须具有所需上传位置的写入权限。虚拟用户也需要此设置进行上传; 默认情况下，虚拟用户被处理为匿名（即最大限制）权限。
默认值：NO

anon_world_readable_only
启用后，只允许匿名用户下载世界可读的文件。这意味着ftp用户可能拥有文件，特别是在上传的情况下。
默认值：是

anonymous_enable
控制是否允许匿名登录。如果启用，用户名 ftp 和 匿名 将被识别为匿名登录。
默认值：是

ascii_download_enable
启用后，ASCII模式数据传输将在下载时得到遵守。
默认值：NO

ascii_upload_enable
启用后，ASCII模式数据传输将在上传时保持。
默认值：NO

async_abor_enable
启用时，将启用一个称为“异步ABOR”的特殊FTP命令。只有不客气的FTP客户端才会使用此功能。另外，这个功能很难处理，所以默认情况下是禁用的。不幸的是，某些FTP客户端将在取消转移时挂起，除非此功能可用，否则可能希望启用它。
默认值：NO

背景
启用时，vsftpd以“监听”模式启动，vsftpd将以侦听器进程为背景。即控制将立即返回到启动vsftpd的shell。
默认值：NO

check_shell
注意！此选项仅对vsftpd的非PAM版本有效。如果禁用，vsftpd将不会检查用于本地登录的有效用户shell的/ etc / shells。
默认值：是

chmod_enable
启用后，允许使用SITE CHMOD命令。注意！这仅适用于本地用户。匿名用户永远不会使用SITE CHMOD。
默认值：是

chown_uploads
如果启用，所有匿名上传的文件将所有权更改为设置chown_username中指定的用户 。这在管理和安全方面都是有用的。
默认值：NO

chroot_list_enable
如果激活，您可以在登录时提供在主目录中放置在chroot（）监狱中的本地用户的列表。如果chroot_local_user设置为YES，则其含义略有不同。在这种情况下，列表将成为不被放置在chroot（）jail中的用户列表。默认情况下，包含此列表的文件是/etc/vsftpd.chroot_list，但您可以使用chroot_list_file 设置来覆盖此列表 。
默认值：NO

chroot_local_user
如果设置为YES，则登录后，本地用户将（默认情况下）放置在其主目录中的chroot（）监控器中。 警告： 此选项具有安全隐患，特别是如果用户具有上传权限或shell访问权限。只有当你知道你在做什么才能启用 请注意，这些安全性影响不是vsftpd特定的。它们适用于提供将本地用户置于chroot（）jail中的所有FTP守护程序。
默认值：NO

connect_from_port_20
这可以控制端口样式数据连接是否在服务器上使用端口20（ftp-data）。出于安全考虑，有些客户可能会坚持认为是这样。相反，禁用此选项可使vsftpd运行的权限略低。
默认值：NO（但是示例配置文件启用它）

debug_ssl
如果为true，OpenSSL连接诊断将转储到vsftpd日志文件。（在v2.0.6中添加）。
默认值：NO

delete_failed_uploads
如果为true，则会删除任何失败的上传文件。（在v2.0.7中添加）。
默认值：NO

deny_email_enable
如果激活，您可能会提供匿名密码电子邮件响应的列表，导致登录被拒绝。默认情况下，包含此列表的文件为/etc/vsftpd.banned_emails，但您可以使用banned_email_file 设置来覆盖此列表 。
默认值：NO

dirlist_enable
如果设置为NO，则所有目录列表命令将给予拒绝的权限。
默认值：是

dirmessage_enable
如果启用，FTP服务器的用户在首次输入新目录时可以显示消息。默认情况下，将扫描文件.message的目录，但可能会使用配置设置 message_file覆盖目录。
默认值：NO（但是示例配置文件启用它）

download_enable
如果设置为NO，则所有下载请求都将被拒绝。
默认值：是

dual_log_enable
如果启用，则会并行生成两个日志文件，默认为 / var / log / xferlog 和 /var/log/vsftpd.log。前者是一个wu-ftpd样式转移日志，可通过标准工具解析。后者是vsftpd自己的风格日志。
默认值：NO

force_dot_files
如果激活，文件和目录以。即使客户端没有使用“a”标志，也会显示在目录列表中。此覆盖不包括“。” 和“..”条目。
默认值：NO

force_anon_data_ssl
仅适用于 ssl_enable 激活。如果激活，所有匿名登录将被强制使用安全的SSL连接，以便在数据连接上发送和接收数据。
默认值：NO

force_anon_logins_ssl
仅适用于 ssl_enable 激活。如果激活，所有匿名登录将被强制使用安全的SSL连接以发送密码。
默认值：NO

force_local_data_ssl
仅适用于 ssl_enable 激活。如果激活，所有非匿名登录将被强制使用安全的SSL连接，以便在数据连接上发送和接收数据。
默认值：是

force_local_logins_ssl
仅适用于 ssl_enable 激活。如果激活，所有非匿名登录将被强制使用安全的SSL连接以发送密码。
默认值：是

guest_enable
如果启用，所有非匿名登录名都将被归类为“访客”登录。客人登录将重新映射到guest_username 设置中指定的用户 。
默认值：NO

hide_ids
如果启用，目录列表中的所有用户和组信息将显示为“ftp”。
默认值：NO

implicit_ssl
如果启用，则SSL握手是所有连接（FTPS协议）首先需要的。为了支持显式的SSL和/或纯文本，应该运行单独的vsftpd侦听器进程。
默认值：NO

听
如果启用，vsftpd将以独立模式运行。这意味着vsftpd不能从某种inetd运行。相反，vsftpd可执行文件直接运行一次。vsftpd本身将会处理侦听和处理传入连接。
默认值：是

listen_ipv6
像listen参数一样，除了vsftpd将侦听IPv6套接字，而不是IPv4侦听。该参数和listen参数是互斥的。
默认值：NO

local_enable
控制是否允许本地登录。如果启用，可以使用/ etc / passwd（或者PAM配置引用的任何地方）中的普通用户帐户进行登录。对于任何非匿名登录，包括虚拟用户都必须启用此功能。
默认值：NO

lock_upload_files
启用后，所有上传都会在上传文件上进行写入锁定。所有下载都会在下载文件上进行共享读锁。警告！在启用此功能之前，请注意，恶意读者可能会使想要添加文件的作者饿死。
默认值：是

log_ftp_protocol
启用后，将记录所有FTP请求和响应，提供xferlog_std_format选项未启用。适用于调试
默认值：NO

ls_recurse_enable
启用后，此设置将允许使用“ls -R”。这是一个小的安全风险，因为大型站点顶层的ls -R可能会消耗大量资源。
默认值：NO

mdtm_write
启用后，此设置将允许MDTM设置文件修改时间（取决于通常的访问检查）。
默认值：是

no_anon_password
启用后，这将阻止vsftpd要求匿名密码 - 匿名用户将直接登录。
默认值：NO

no_log_lock
启用时，这将阻止vsftpd在写入日志文件时采取文件锁定。通常不应该启用此选项。它存在于解决操作系统错误，例如已经被观察到的Solaris / Veritas文件系统组合，有时会出现试图锁定日志文件的挂起。
默认值：NO

one_process_model
如果您有一个Linux 2.4内核，可以使用不同的安全模型，每个连接只使用一个进程。这是一个不太纯粹的安全模式，但是获得了你的表现。您真的不想启用此功能，除非您知道自己在做什么，并且您的站点支持大量同时连接的用户。
默认值：NO

passwd_chroot_enable
如果启用，以及 chroot_local_user ，则可以在每个用户的基础上指定chroot（）监狱位置。每个用户的监狱都是从/ etc / passwd中的主目录字符串派生出来的。主目录字符串中的/./的出现表示该监狱位于路径中的特定位置。
默认值：NO

pasv_addr_resolve
如果要在pasv_address 选项中使用主机名（而不是IP地址），请设置为YES 。
默认值：NO

pasv_enable
如果要禁止PASV方法获取数据连接，请设置为NO。
默认值：是

pasv_promiscuous
如果要禁用PASV安全检查，确保数据连接来自与控制连接相同的IP地址，请设置为YES。只有当你知道你在做什么才能启用 唯一合法的用途是采用某种形式的安全隧道方案，或者是为了方便FXP的支持。
默认值：NO

port_enable
如果您不想使用PORT方法获取数据连接，则设置为NO。
默认值：是

port_promiscuous
如果要禁用PORT安全检查，确保传出数据连接只能连接到客户端，请设置为YES。只有当你知道你在做什么才能启用
默认值：NO

require_cert
如果设置为yes，则需要所有SSL客户端连接才能提供客户端证书。此证书的验证程度由 validate_cert （v2.0.6中添加）控制。
默认值：NO

require_ssl_reuse
如果设置为yes，则需要所有SSL数据连接才能展示SSL会话重用（这证明他们知道与控制通道相同的主密钥）。虽然这是一个安全的默认值，但它可能会破坏许多FTP客户端，因此您可能需要禁用它。有关后果的讨论，请参阅 http://scarybeastsecurity.blogspot.com/2009/02/vsftpd-210-released.html （在v2.1.0中添加）。
默认值：是

run_as_launching_user
如果您希望vsftpd作为启动vsftpd的用户运行，请设置为YES。这在root访问不可用时很有用。大量警告！不要启用此选项，除非您完全知道您正在做什么，因为天真使用此选项可能会产生大量的安全问题。具体来说，当设置此选项（即使由root启动）时，vsftpd不会/不能使用chroot技术来限制文件访问。一个糟糕的替代品可能是使用一个 deny_file 设置，如{/*,*..*}，但是它的可靠性与chroot无法比较，不应该依赖。如果使用此选项，则适用其他选项的许多限制。例如，不需要特权的选项，例如非匿名登录，上传所有权更改，从端口20连接和监听端口小于1024的选项不会有效。
默认值：NO

secure_email_list_enable
如果您只想要接受匿名登录的电子邮件密码的指定列表，请设置为YES。这是一种低成本的方式，无需虚拟用户即可限制对低安全性内容的访问。启用后，除非提供的密码列在email_password_file 设置指定的文件中，否则将阻止匿名登录 。文件格式是每行一个密码，没有额外的空格。默认文件名为/etc/vsftpd.email_passwords。
默认值：NO

session_support
这将控制vsftpd是否尝试维护登录的会话。如果vsftpd正在维护会话，它将尝试更新utmp和wtmp。如果使用PAM验证，它也会打开一个pam_session，并且只有在注销时关闭它。如果您不需要会话日志记录，您可能希望禁用此功能，并且希望给予vsftpd更多机会以更少的进程和/或更少的权限运行。注意 - 只有在支持PAM的版本中才能提供utmp和wtmp支持。
默认值：NO

setproctitle_enable
如果启用，vsftpd将尝试在系统进程列表中显示会话状态信息。换句话说，报告的进程名称将会更改，以反映vsftpd会话正在做什么（空闲，下载等）。为安全起见，您可能希望将其关闭。
默认值：NO

ssl_request_cert
如果启用，vsftpd会要求（但不一定需要;见 require_cert）一个证书上的传入 SSL 连接。通常这 不应该造成任何麻烦，但IBM zOS似乎有问题。（v2.0.7中的新增）。
默认值：是

ssl_sslv2
仅适用于 ssl_enable 激活。如果启用，此选项将允许SSL v2协议连接。TLS v1连接是首选。
默认值：NO

ssl_sslv3
仅适用于 ssl_enable 激活。如果启用，此选项将允许SSL v3协议连接。TLS v1连接是首选。
默认值：NO

ssl_tlsv1
仅适用于 ssl_enable 激活。如果启用，此选项将允许TLS v1协议连接。TLS v1连接是首选。
默认值：是

strict_ssl_read_eof
如果启用，SSL数据上传需要通过SSL终止，而不是套接字上的EOF。需要此选项以确保攻击者没有使用假的TCP FIN提前终止上传。不幸的是，它没有默认启用，因为很少的客户端正确。（v2.0.7中的新增）。
默认值：NO

strict_ssl_write_shutdown
如果启用，SSL数据下载需要通过SSL终止，而不是套接字上的EOF。这是默认关闭，因为我无法找到一个单一的FTP客户端这样做。这是小事 所有这一切都是我们能够判断客户端是否确认完整收到该文件的能力。即使没有此选项，客户端也可以检查下载的完整性。（v2.0.7中的新增）。
默认值：NO

syslog_enable
如果启用，则将会转到/var/log/vsftpd.log的任何日志输出转到系统日志。日志记录是在FTPD设备下完成的。
默认值：NO

tcp_wrappers的
如果启用，并且vsftpd已使用tcp_wrappers支持进行编译，则传入连接将通过tcp_wrappers访问控制进行。此外，还有一种基于IP的配置机制。如果tcp_wrappers设置VSFTPD_LOAD_CONF环境变量，则vsftpd会话将尝试加载此变量中指定的vsftpd配置文件。
默认值：NO

text_userdb_names
默认情况下，数字ID显示在目录列表的用户和组字段中。您可以通过启用此参数来获取文本名称。由于性能原因，它默认关闭。
默认值：NO

tilde_user_enable
如果启用，vsftpd将尝试解析路径名，例如〜chris / pics，即一个波浪号，后跟一个用户名。请注意，vsftpd将始终解析路径名〜和〜/ something（在这种情况下〜解析为初始登录目录）。注意〜〜用户路径只有 在_current_ chroot（）jail中可能找到/ etc / passwd文件时才会解析 。
默认值：NO

use_localtime
如果启用，vsftpd将显示当前时区的目录列表。默认是显示GMT。MDTM FTP命令返回的时间也受此选项的影响。
默认值：NO

use_sendfile
用于测试在您的平台上使用sendfile（）系统调用的相对优势的内部设置。
默认值：是

userlist_deny
如果userlist_enable 被激活，则会检查此选项 。如果您设置此设置为NO，那么用户将无法登录，除非它们被指定的文件中明确列出 userlist_file。拒绝登录时，在用户被要求输入密码之前发出拒绝。
默认值：是

userlist_enable
如果启用，vsftpd将从userlist_file提供的文件名加载用户名 列表。如果用户尝试使用此文件中的名称登录，则在被要求输入密码之前将被拒绝。这可能有助于防止正在发送的明文密码。另请参阅 userlist_deny。
默认值：NO

validate_cert
如果设置为yes，则所有接收到的SSL客户端证书必须验证OK。自签名证书不构成OK验证。（v2.0.6中的新功能）。
默认值：NO

virtual_use_local_privs
如果启用，虚拟用户将使用与本地用户相同的权限。默认情况下，虚拟用户将使用与匿名用户相同的权限，这往往会受到更多限制（特别是在写访问方面）。
默认值：NO

WRITE_ENABLE
这可以控制是否允许更改文件系统的FTP命令。这些命令是：STOR，DELE，RNFR，RNTO，MKD，RMD，APPE和SITE。
默认值：NO

xferlog_enable
如果启用，将保留一个日志文件，禁止上传和下载。默认情况下，此文件将放置在/var/log/vsftpd.log中，但可能会使用配置设置vsftpd_log_file覆盖该位置 。
默认值：NO（但是示例配置文件启用它）

xferlog_std_format
如果启用，传输日志文件将以wu-ftpd使用的标准xferlog格式写入。这是有用的，因为您可以重用现有的传输统计信息生成器。然而，默认格式更易于阅读。这种风格的日志文件的默认位置是/ var / log / xferlog，但您可以使用设置xferlog_file更改它 。
默认值：NO


数字选项

以下是数字选项列表。数字选项必须设置为非负整数。为了方便umask选项，支持八进制数。要指定八进制数，请使用0作为数字的第一位。
accept_timeout
远程客户端建立与PASV样式数据连接的连接的超时（以秒为单位）。
默认值：60

anon_max_rate
匿名客户端允许的最大数据传输速率（以字节为单位）。
默认值：0（无限制）

anon_umask
为匿名用户设置文件创建的umask的值。注意！如果要指定八进制值，请记住“0”前缀，否则该值将被视为基数10整数！
默认值：077

chown_upload_mode
要强制为chown（）的文件模式进行匿名上传。（在v2.0.6中添加）。
默认值：0600

connect_timeout
远程客户端响应我们的端口样式数据连接的超时时间（秒）。
默认值：60

data_connection_timeout
超时时间（以秒为单位），大概是允许数据传输停止而无进度的最大时间。如果超时触发，远程客户端将被启动。
默认值：300

delay_failed_login
报告登录失败之前暂停的秒数。
默认值：1

delay_successful_login
允许成功登录之前暂停的秒数。
默认值：0

file_open_mode
创建上传文件的权限。Umasks应用于此值的顶部。如果要上传的文件可执行，您可能希望更改为0777。
默认值：0666

ftp_data_port
端口样式连接始发的端口（只要名称不 正确的connect_from_port_20 启用）。
默认值：20

idle_session_timeout
远程客户端可能在FTP命令之间花费的最长时间（以秒为单位）。如果超时触发，远程客户端将被启动。
默认值：300

listen_port
如果vsftpd处于独立模式，则这是它将侦听传入FTP连接的端口。
默认值：21

local_max_rate
本地认证用户允许的最大数据传输速率（以字节为单位）。
默认值：0（无限制）

local_umask
为本地用户设置文件创建的umask的值。注意！如果要指定八进制值，请记住“0”前缀，否则该值将被视为基数10整数！
默认值：077

max_clients
如果vsftpd处于独立模式，则这是可能连接的最大客户端数。连接的任何其他客户端将收到一条错误消息。
默认值：0（无限制）

max_login_fails
在这么多登录失败之后，会话被杀死。
默认值：3

max_per_ip
如果vsftpd处于独立模式，则可以从相同的源Internet地址连接的最大客户端数。如果客户端超过此限制，则会收到错误消息。
默认值：0（无限制）

pasv_max_port
为PASV样式数据连接分配的最大端口。可用于指定窄端口范围以辅助防火墙。
默认值：0（使用任何端口）

pasv_min_port
为PASV样式数据连接分配的最小端口。可用于指定窄端口范围以辅助防火墙。
默认值：0（使用任何端口）

trans_chunk_size
你可能不想改变这一点，但是尝试将其设置为像8192那样更平滑的带宽限制器。
默认值：0（让vsftpd选择合理的设置）


STRING选项

以下是字符串选项列表。
anon_root
此选项表示vsftpd将在匿名登录后尝试更改的目录。失败被忽略。
默认值：（无）

banned_email_file
此选项是包含不允许的匿名电子邮件密码列表的文件的名称。如果 启用了选项deny_email_enable，则会查询该文件 。
默认值：/etc/vsftpd.banned_emails

banner_file
此选项是包含有人连接到服务器时要显示的文本的文件的名称。如果设置，它将覆盖由ftpd_banner 选项提供的横幅字符串 。
默认值：（无）

ca_certs_file
此选项是为了验证客户端证书的目的，加载证书颁发机构证书的文件的名称。遗憾的是，由于vsftpd使用受限文件系统空间（chroot），因此不使用默认的SSL CA cert路径。（在v2.0.6中添加）。
默认值：（无）

chown_username
这是匿名上传文件的所有权的用户的名称。只有另一个选项chown_uploads被设置，这个选项才是 有用的。
默认值：root

chroot_list_file
该选项是包含本地用户列表的文件的名称，该列表将被放置在其主目录中的chroot（）监狱中。仅当 启用了chroot_list_enable选项时，此选项才相关 。如果 启用了选项 chroot_local_user，则列表文件将成为不放置在chroot（）jail中的用户列表。
默认值：/etc/vsftpd.chroot_list

cmds_allowed
此选项指定允许的FTP命令的逗号分隔列表（登录后，USER，PASS和QUIT等）始终允许预登录。其他命令被拒绝。这是真正锁定FTP服务器的强大方法。示例：cmds_allowed = PASV，RETR，QUIT
默认值：（无）

cmds_denied
此选项指定以逗号分隔的被拒绝的FTP命令列表（登录后，用户，PASS，QUIT等）始终允许预登录。如果这两个命令和cmds_allowed都出现， 则拒绝优先。（在v2.1.0中添加）。
默认值：（无）

deny_file
此选项可用于设置不能以任何方式访问的文件名（和目录名称等）的模式。受影响的项目不会被隐藏，但任何尝试对其进行任何操作（下载，更改为目录，影响目录等内容）将被拒绝。此选项非常简单，不应用于严重的访问控制 - 应优先使用文件系统的权限。但是，此选项在某些虚拟用户设置中可能很有用。特别知道如果文件名可以通过各种名称访问（可能是由于符号链接或硬链接），则必须小心拒绝访问所有名称。如果其名称包含由hide_file给出的字符串，或者它们与hide_file指定的正则表达式匹配，那么访问将被拒绝。请注意，vsftpd' 正则表达式匹配代码是一个简单的实现，它是完整的正则表达式功能的一个子集。因此，您将需要仔细和详尽地测试此选项的任何应用程序。由于其可靠性更高，因此建议您对任何重要的安全策略使用文件系统权限。支持的正则表达式语法是*，？和未知的{，}运算符。正则表达式匹配仅在路径的最后一个组件上支持，例如a / b /？被支持，但是/？/ c不是。示例：deny_file = {*。mp3，*。mov，.private} 由于其可靠性更高，因此建议您对任何重要的安全策略使用文件系统权限。支持的正则表达式语法是*，？和未知的{，}运算符。正则表达式匹配仅在路径的最后一个组件上支持，例如a / b /？被支持，但是/？/ c不是。示例：deny_file = {*。mp3，*。mov，.private} 由于其可靠性更高，因此建议您对任何重要的安全策略使用文件系统权限。支持的正则表达式语法是*，？和未知的{，}运算符。正则表达式匹配仅在路径的最后一个组件上支持，例如a / b /？被支持，但是/？/ c不是。示例：deny_file = {*。mp3，*。mov，.private}
默认值：（无）

dsa_cert_file
此选项指定要用于SSL加密连接的DSA证书的位置。
默认值：（无 - RSA证书足够）

dsa_private_key_file
此选项指定用于SSL加密连接的DSA私钥的位置。如果未设置此选项，则预期私钥与证书位于同一文件中。
默认值：（无）

email_password_file
此选项可用于为secure_email_list_enable 设置的使用提供备用文件 。
默认值：/etc/vsftpd.email_passwords

ftp_username
这是用于处理匿名FTP的用户的名称。该用户的主目录是匿名FTP区域的根目录。
默认值：ftp

ftpd_banner
此字符串选项允许您重写连接第一次进入时由vsftpd显示的问候语标题。
默认值：（无 - 显示默认vsftpd横幅）

guest_username
有关 什么构成访客登录的说明，请参阅guest_enable的布尔值设置 。此设置是访客用户映射到的真实用户名。
默认值：ftp

hide_file
此选项可用于为目录列表隐藏的文件名（和目录名称等）设置模式。尽管被隐藏，文件/目录等可以完全访问谁知道什么名字实际使用的客户。如果它们的名称包含由hide_file给出的字符串，或者它们与hide_file指定的正则表达式匹配，则项目将被隐藏。请注意，vsftpd的正则表达式匹配代码是一个简单的实现，它是完整的正则表达式功能的一个子集。见 deny_file 为正是正则表达式语法支持的细节。示例：hide_file = {*。mp3，.hidden，hide *，h？}
默认值：（无）

listen_address
如果vsftpd处于独立模式，则可以通过此设置覆盖默认监听地址（所有本地接口）。提供数字IP地址。
默认值：（无）

listen_address6
像listen_address一样，但是为IPv6侦听器指定了一个默认侦听地址（如果设置了listen_ipv6则使用该地址）。格式是标准的IPv6地址格式。
默认值：（无）

local_root
此选项表示在本地（即非匿名）登录后vsftpd将尝试更改的目录。失败被忽略。
默认值：（无）

message_file
此选项是输入新目录时查找的文件的名称。内容显示给远程用户。仅当 启用了选项dirmessage_enable时，此选项才相关 。
默认值：.message

nopriv_user
这是VSftpd在完全无特权时使用的用户的名称。请注意，这应该是一个专门的用户，而不是没有人。用户在大多数机器上没有人倾向于使用很多重要的事情。
默认值：nobody

pam_service_name
该字符串是vsftpd将使用的PAM服务的名称。
默认值：ftp

pasv_address设置
使用此选项覆盖vsftpd将响应PASV命令通告的IP地址。提供数字IP地址，除非 启用了pasv_addr_resolve，在这种情况下，您可以提供一个在启动时为您解析的主机名。
默认值：（无 - 地址取自已连接的插座）

rsa_cert_file
此选项指定用于SSL加密连接的RSA证书的位置。
默认值：/usr/share/ssl/certs/vsftpd.pem

rsa_private_key_file
此选项指定用于SSL加密连接的RSA私钥的位置。如果未设置此选项，则预期私钥与证书位于同一文件中。
默认值：（无）

secure_chroot_dir
此选项应为空的目录的名称。此外，ftp用户不能写入该目录。此目录用作安全chroot（）监狱，vsftpd不需要文件系统访问。
默认值：/ usr / share / empty

的ssl_ciphers
此选项可用于选择哪些SSL密码vsftpd将允许加密的SSL连接。有关 详细信息，请参阅 密码手册页。请注意，限制密码可能是一个有用的安全措施，因为它可以防止恶意的远程方强制发现问题的密码。
默认值：DES-CBC3-SHA

user_config_dir
这个强大的选项允许在每个用户的基础上覆盖手册页面中指定的任何配置选项。用法很简单，最好用一个例子说明。如果将 user_config_dir 设置为 / etc / vsftpd_user_conf ，然后以用户“chris”身份登录，则vsftpd将 在会话期间将文件/ etc / vsftpd_user_conf / chris中的设置应用于此 。此文件的格式在本手册页中详细说明！请注意，并非所有设置在每个用户的基础上都有效。例如，仅在用户会话开始之前进行许多设置。不会影响每个用户的任何行为的设置示例包括listen_address，banner_file，max_per_ip，max_clients，xferlog_file等。
默认值：（无）

user_sub_token
此选项与虚拟用户结合使用非常有用。它用于根据模板为每个虚拟用户自动生成主目录。例如，如果通过guest_username指定的真实用户的主 目录 是 / home / virtual / $ USER，而 user_sub_token 设置为 $ USER，则当虚拟用户fred登录时，他将最终（通常是chroot（）' ）在/ home / virtual / fred目录中 。如果local_root 包含 user_sub_token，此选项也会生效 。
默认值：（无）

userlist_file
此选项是当userlist_enable 选项处于活动状态时加载的文件的名称 。
默认值：/etc/vsftpd.user_list

vsftpd_log_file
此选项是我们编写vsftpd样式日志文件的文件的名称。只有 设置了xferlog_enable选项，而且xferlog_std_format 未设置， 才会写入该日志 。或者，如果您设置了选项 dual_log_enable，则会写入。还有一个更复杂的问题 - 如果你设置了 syslog_enable，那么这个文件不会被写入，而是把它输出到系统日志。
默认值：/var/log/vsftpd.log

xferlog_file
此选项是我们编写wu-ftpd样式传输日志的文件的名称。传输日志仅在xferlog_enable选项 设置以及 xferlog_std_format时才会写入 。或者，如果您设置了选项 dual_log_enable，则会写入。
默认值：/ var / log / xferlog

```
## vsftpd ##
该文档为vsftpd使用PAM模块时的相关配置文件，它的实际目录为`/etc/pam.d/vsftpd`
## ftpusers ##
该文档为vsftpd拒绝登录用户的清单，也就是上面PAM模块中配置所指向的目录，它的实际目录为`/etc/vsftpd/ftpusers`
## user_list ##
该文档为vsftpd登录白名单/黑名单的清单，其是否生效以及是白名单/黑名单取决于vsftpd.conf的配置，它的实际目录为`/etc/vsftpd/user_list`
## chroot_list ##
该文档为vsftpd限制用户根目录的清单，其是否生效取决于vsftpd.conf的配置，它的实际目录为`/etc/vsftpd/chroot_list`

> # Vsftp使用 #

> # Vsftp参考文档 #
