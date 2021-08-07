越狱 iOS 系统内存限制修改

越狱后的 iOS 系统在使用 Kitsunebi 时会有崩溃的情况，目前来看是与内存限制有关，越狱系统似乎更容易触发内存上限导致应用被系统杀掉。

在 iOS 中负责监控其它进程内存用量和杀掉超出限制的进程叫做 Jetsam，在它的配置文件中就有相关的对内存做限制的配置，它的配置文件一般在 /System/Library/LaunchDaemons/com.apple.jetsamproperties.{Model}.plist，其中 Model 在各个手机上可能都不一样，也有可能有多个这样的文件。里面对 VPN 进程做限制的条目是：

			<key>com.apple.networkextension.packet-tunnel</key>
			<dict>
				<key>ActiveHardMemoryLimit</key>
				<integer>15</integer>
				<key>InactiveHardMemoryLimit</key>
				<integer>15</integer>
				<key>JetsamPriority</key>
				<integer>14</integer>
			</dict>
打开文件后搜索 packet-tunnel 即可找到，其中两个 15 的数值就是 iOS 对 VPN 进程的内存限制值 15MB。

要修改 iOS VPN 进程的内存限制，我们只需要用 iFile 等文件管理工具找到这些配置文件，复制到电脑上然后对相关数值进行修改，修改后覆盖原来文件，重启一下手机即可。

要打开这些 plist 文件需要一些特殊的编辑器；如果你用的是 macOS，且安装有 Xcode，那就可以直接双击打开，如果没装 Xcode，可以下载 BBEdit(30 天试用期) 这个软件来打开；如果你用的是 Windows，大概可以使用 这个 软件来编辑。

要修改的内容很明显了，就是把数值改大就行，比如把原本 15MB 的限制改为 30MB 限制：

			<key>com.apple.networkextension.packet-tunnel</key>
			<dict>
				<key>ActiveHardMemoryLimit</key>
				<integer>30</integer>
				<key>InactiveHardMemoryLimit</key>
				<integer>30</integer>
				<key>JetsamPriority</key>
				<integer>14</integer>
			</dict>
