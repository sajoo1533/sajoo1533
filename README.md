sajoo1533
/
README.md
in
main

Edit

Preview
Sign up iranxray / hope Public Code Issues 32 More Jump to bottom استفاده از ورکر کلادفلر و گرفتن کانفیگ های رایگان #71 Open hamihastam opened this issue on Feb 23 · 3 comments Open استفاده از ورکر کلادفلر و گرفتن کانفیگ های رایگان #71 hamihastam opened this issue on Feb 23 · 3 comments Comments hamihastam commented on Feb 23 سلام این آموزش رو از توییتر برداشتم و به نظرم بهترین راه برای گرفتن کانفیگ رایگان v2ray هست.

https://twitter.com/vahidfarid/status/1628313909273808898?s=46&t=s3n-vutdHS2PtBJ95LaFxQ

اول برید سایت workers.cloudflare.com ثبت نام کنید و ایمیلتون رو وریفای کنید. طبق عکسا ادامه بدید. 19E91206-FEF1-4084-AEC2-026BB31FB3B7

E76610AB-FC0E-4EFF-9878-AAE020074E3E

![87CB0BBA-E2AB-4DB8-99A4-3D9B67F7B221](https://user-images.githubusercontent.com/120744411/220751689-f577626a-4b86-4ba2-8de5- 427290cfe17f.jpeg)

80BD184E-AA11-469A-BD4A-3CFB38F005B7

EC2666C9-A8FC-4E9E-A5A4-EB1CC799A04A این متن رو کپی کنید و اینجا پیست کنید.

const subLink1 = "https://raw.githubusercontent.com/freefq/free/master/v2" const subLink2 = "https://raw.githubusercontent.com/Pawdroid/Free-servers/main/sub" const cnfLink1 = "https://raw.githubusercontent.com/mahdibland/ShadowsocksAggregator/master/sub/sub_merge.txt" const cleanIPLink = "http://bot.sudoer.net/best.cf.iran.all" const operatorList = ["AST", "HWB", "IRC", "MBT", "MCI", "MKB", "PRS", "RTL", "SHT", "ZTL"] const addressList = ["discord.com", "cloudflare.com", "nginx.com", "cdnjs.com", "vimeo.com", "networksolutions.com", "spotify.com"] const fpList = ["chrome", "chrome", "chrome", "firefox", "safari", "edge", "ios", "android", "random", "random"] const alpnList = ["http/1.1", "h2,http/1.1", "h2,http/1.1"]

export default { async fetch(request) { var url = new URL(request.url) var pathParts = url.pathname.replace(/^/|/$/g, "").split("/") if (pathParts[0] == "sub") { var cleanIPs = [] if (pathParts[1] !== undefined) { var operator = pathParts[1].toUpperCase() if (operatorList.includes(operator)) { cleanIPs = await fetch(cleanIPLink).then(r => r.text()).then(t => t.split("\n")) cleanIPs = cleanIPs.filter(line => (line.search(operator) > 0)) cleanIPs = cleanIPs.map(line => line.split(" ")[0].trim()) } else if (isIp(operator)) { cleanIPs = [operator] } } var configList = [] configList = configList.concat(await fetch(subLink1).then(r => r.text()).then(a => atob(a)).then(t => t.split("\n"))) configList = configList.concat(await fetch(subLink2).then(r => r.text()).then(a => atob(a)).then(t => t.split("\n"))) configList = configList.concat(await fetch(cnfLink1).then(r => r.text()).then(t => t.split("\n"))) configList = configList.filter(cnf => (cnf.search("vmess://") == 0)) configList = configList.map(config => { try { var conf = JSON.parse(atob(config.substr(8))) if (conf.tls != "tls") { throw "no-tls" } var addr = conf.sni if (!addr) { if (conf.add && !isIp(conf.add)) { addr = conf.add } else if (conf.host && !isIp(conf.host)) { addr = conf.host } } if (!addr) { throw "no-tls" } conf.sni = url.hostname if (cleanIPs.length) { conf.add = cleanIPs[Math.floor(Math.random() * cleanIPs.length)] } else { conf.add = addressList[Math.floor(Math.random() * addressList.length)] } conf.host = url.hostname conf.path = "/" + addr + ":" + conf.port + conf.path conf.fp = fpList[Math.floor(Math.random() * fpList.length)] conf.alpn = alpnList[Math.floor(Math.random() * alpnList.length)] conf.port = 443 return "vmess://" + btoa(JSON.stringify(conf)) } catch (e) { return "" } }) configList = getMultipleRandomElements(configList.filter(cnf => (cnf.length > 10)), 100) return new Response(btoa(configList.join("\n"))); } else { var url = new URL(request.url) var newUrl = new URL("https://" + url.pathname.replace(/^/|/$/g, '')) return fetch(new Request(newUrl, request)); } } }

function getMultipleRandomElements(arr, num) { var shuffled = [...arr].sort(() => 0.5 - Math.random()); return shuffled.slice(0, num); }

function isIp(str) { try { if (str == "" || str == undefined) return false; if (!/^(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])(.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])){2}.(\d{1,2}|1\d\d|2[0-4]\d|25[0-4])$/.test(str)) { return false; } var ls = str.split('.'); if (ls == null || ls.length != 4 || ls[3] == "0" || parseInt(ls[3]) === 0) { return false; } return true; } catch (ee) { } return false; }sajoo1533
/
README.md
in
main

Edit

Preview
Sign up iranxray / hope Public Code Issues 32 More Jump to bottom استفاده از ورکر کلادفلر و گرفتن کانفیگ های رایگان #71 Open hamihastam opened this issue on Feb 23 · 3 comments Open استفاده از ورکر کلادفلر و گرفتن کانفیگ های رایگان #71 hamihastam opened this issue on Feb 23 · 3 comments Comments hamihastam commented on Feb 23 سلام این آموزش رو از توییتر برداشتم و به نظرم بهترین راه برای گرفتن کانفیگ رایگان v2ray هست.

https://twitter.com/vahidfarid/status/1628313909273808898?s=46&t=s3n-vutdHS2PtBJ95LaFxQ

اول برید سایت workers.cloudflare.com ثبت نام کنید و ایمیلتون رو وریفای کنید. طبق عکسا ادامه بدید. 19E91206-FEF1-4084-AEC2-026BB31FB3B7

E76610AB-FC0E-4EFF-9878-AAE020074E3E

![87CB0BBA-E2AB-4DB8-99A4-3D9B67F7B221](https://user-images.githubusercontent.com/120744411/220751689-f577626a-4b86-4ba2-8de5- 427290cfe17f.jpeg)

80BD184E-AA11-469A-BD4A-3CFB38F005B7

EC2666C9-A8FC-4E9E-A5A4-EB1CC799A04A این متن رو کپی کنید و اینجا پیست کنید.

const subLink1 = "https://raw.githubusercontent.com/freefq/free/master/v2" const subLink2 = "https://raw.githubusercontent.com/Pawdroid/Free-servers/main/sub" const cnfLink1 = "https://raw.githubusercontent.com/mahdibland/ShadowsocksAggregator/master/sub/sub_merge.txt" const cleanIPLink = "http://bot.sudoer.net/best.cf.iran.all" const operatorList = ["AST", "HWB", "IRC", "MBT", "MCI", "MKB", "PRS", "RTL", "SHT", "ZTL"] const addressList = ["discord.com", "cloudflare.com", "nginx.com", "cdnjs.com", "vimeo.com", "networksolutions.com", "spotify.com"] const fpList = ["chrome", "chrome", "chrome", "firefox", "safari", "edge", "ios", "android", "random", "random"] const alpnList = ["http/1.1", "h2,http/1.1", "h2,http/1.1"]

export default { async fetch(request) { var url = new URL(request.url) var pathParts = url.pathname.replace(/^/|/$/g, "").split("/") if (pathParts[0] == "sub") { var cleanIPs = [] if (pathParts[1] !== undefined) { var operator = pathParts[1].toUpperCase() if (operatorList.includes(operator)) { cleanIPs = await fetch(cleanIPLink).then(r => r.text()).then(t => t.split("\n")) cleanIPs = cleanIPs.filter(line => (line.search(operator) > 0)) cleanIPs = cleanIPs.map(line => line.split(" ")[0].trim()) } else if (isIp(operator)) { cleanIPs = [operator] } } var configList = [] configList = configList.concat(await fetch(subLink1).then(r => r.text()).then(a => atob(a)).then(t => t.split("\n"))) configList = configList.concat(await fetch(subLink2).then(r => r.text()).then(a => atob(a)).then(t => t.split("\n"))) configList = configList.concat(await fetch(cnfLink1).then(r => r.text()).then(t => t.split("\n"))) configList = configList.filter(cnf => (cnf.search("vmess://") == 0)) configList = configList.map(config => { try { var conf = JSON.parse(atob(config.substr(8))) if (conf.tls != "tls") { throw "no-tls" } var addr = conf.sni if (!addr) { if (conf.add && !isIp(conf.add)) { addr = conf.add } else if (conf.host && !isIp(conf.host)) { addr = conf.host } } if (!addr) { throw "no-tls" } conf.sni = url.hostname if (cleanIPs.length) { conf.add = cleanIPs[Math.floor(Math.random() * cleanIPs.length)] } else { conf.add = addressList[Math.floor(Math.random() * addressList.length)] } conf.host = url.hostname conf.path = "/" + addr + ":" + conf.port + conf.path conf.fp = fpList[Math.floor(Math.random() * fpList.length)] conf.alpn = alpnList[Math.floor(Math.random() * alpnList.length)] conf.port = 443 return "vmess://" + btoa(JSON.stringify(conf)) } catch (e) { return "" } }) configList = getMultipleRandomElements(configList.filter(cnf => (cnf.length > 10)), 100) return new Response(btoa(configList.join("\n"))); } else { var url = new URL(request.url) var newUrl = new URL("https://" + url.pathname.replace(/^/|/$/g, '')) return fetch(new Request(newUrl, request)); } } }

function getMultipleRandomElements(arr, num) { var shuffled = [...arr].sort(() => 0.5 - Math.random()); return shuffled.slice(0, num); }

function isIp(str) { try { if (str == "" || str == undefined) return false; if (!/^(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])(.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])){2}.(\d{1,2}|1\d\d|2[0-4]\d|25[0-4])$/.test(str)) { return false; } var ls = str.split('.'); if (ls == null || ls.length != 4 || ls[3] == "0" || parseInt(ls[3]) === 0) { return false; } return true; } catch (ee) { } return false; }
