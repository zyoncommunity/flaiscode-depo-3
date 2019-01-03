const Discord = require('discord.js')
const fs = require('fs');
var ayarlar = require('../ayarlar.json');
let kanal = JSON.parse(fs.readFileSync("././sunucuyaözelayarlar/glog.json", "utf8"));

exports.run = async (client, message, args) => {
if (!message.member.hasPermission("ADMINISTRATOR")) return message.reply(`Bu komutu kullanabilmek için **Yönetici** iznine sahip olmalısın!`);
  
  let channel = message.mentions.channels.first()
    if (!channel) {
        message.channel.send(':x: | Kullanım: `f!gkanal #kanal`')
        return
    }
    if(!kanal[message.guild.id]){
        kanal[message.guild.id] = {
            resim: channel.id
        };
    }
    fs.writeFile("././sunucuyaözelayarlar/glog.json", JSON.stringify(kanal), (err) => {
        console.log(err)
    })
    message.channel.send(`:white_check_mark: | Resimli hg bb kanalı ${channel} olarak ayarlandı.`)
}
    
exports.conf = {
    enabled: true,
    guildOnly: false,
    aliases: [],
    permLevel: 0
}

exports.help = {
    name: 'gkanal',
    description: 'Log kanalını belirler.',
    usage: 'gkanal <#kanal>'
}

//bot.js

client.on("guildMemberAdd", async member => {
   const fs = require('fs');
    let gkanal = JSON.parse(fs.readFileSync("././sunucuyaözelayarlar/glog.json", "utf8"));
    const gözelkanal = member.guild.channels.get(gkanal[member.guild.id].resim)
    if (!gözelkanal) return;
     let username = member.user.username;
        if (gözelkanal === undefined || gözelkanal === null) return;
        if (gözelkanal.type === "text") {
            const bg = await Jimp.read("https://cdn.discordapp.com/attachments/450693709076365323/473184528148725780/guildAdd.png");
            const userimg = await Jimp.read(member.user.avatarURL);
            var font;
            if (member.user.tag.length < 15) font = await Jimp.loadFont(Jimp.FONT_SANS_128_WHITE);
            else if (member.user.tag.length > 15) font = await Jimp.loadFont(Jimp.FONT_SANS_64_WHITE);
            else font = await Jimp.loadFont(Jimp.FONT_SANS_32_WHITE);
            await bg.print(font, 430, 170, member.user.tag);
            await userimg.resize(362, 362);
            await bg.composite(userimg, 43, 26).write("./img/"+ member.id + ".png");
              setTimeout(function () {
                    gözelkanal.send(new Discord.Attachment("./img/" + member.id + ".png"));
              }, 1000);
              setTimeout(function () {
                fs.unlink("./img/" + member.id + ".png");
              }, 10000);
        }
    })
(düzenlendi)
client.on("guildMemberRemove", async member => {
   const fs = require('fs');
    let gkanal = JSON.parse(fs.readFileSync("././sunucuyaözelayarlar/glog.json", "utf8"));
    const gözelkanal = member.guild.channels.get(gkanal[member.guild.id].resim)
    if (!gözelkanal) return;
        let username = member.user.username;
        if (gözelkanal === undefined || gözelkanal === null) return;
        if (gözelkanal.type === "text") {            
                        const bg = await Jimp.read("https://cdn.discordapp.com/attachments/450693709076365323/473184546477572107/guildRemove.png");
            const userimg = await Jimp.read(member.user.avatarURL);
            var font;
            if (member.user.tag.length < 15) font = await Jimp.loadFont(Jimp.FONT_SANS_128_WHITE);
            else if (member.user.tag.length > 15) font = await Jimp.loadFont(Jimp.FONT_SANS_64_WHITE);
            else font = await Jimp.loadFont(Jimp.FONT_SANS_32_WHITE);
            await bg.print(font, 430, 170, member.user.tag);
            await userimg.resize(362, 362);
            await bg.composite(userimg, 43, 26).write("./img/"+ member.id + ".png");
              setTimeout(function () {
                    gözelkanal.send(new Discord.Attachment("./img/" + member.id + ".png"));
              }, 1000);
              setTimeout(function () {
                fs.unlink("./img/" + member.id + ".png");
              }, 10000);
        }
    })