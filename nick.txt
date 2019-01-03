const Discord = require("discord.js");
const fs = require("fs");

module.exports.run = async (bot, message, args) => {
  
  if (!args[0]) return message.channel.send(':basarisiz: | Kullanım: **+nick <Nick>**');
  if (!message.member.hasPermission("MANAGE_NICKNAMES")) return message.channel.send(":basarisiz: | Bu komutu kullanabilmek için **yeterli izne sahip değilsin!**");

  let nicks = JSON.parse(fs.readFileSync("./ayarlar/nick.json", "utf8"));

  nicks[message.guild.id] = {
    nicks: args[0]
  };

  fs.writeFile("./ayarlar/nick.json", JSON.stringify(nicks), (err) => {
    if (err) console.log(err)
  });
  
  message.guild.members.get(bot.user.id).setNickname(args[0])
  
  message.channel.send(`:basarili: | Nick başarıyla \`${args[0]}\` olarak ayarlandı!`)

}

exports.conf = {
  enabled: true,
  guildOnly: true,
  aliases: [],
  permLevel: 0
};

exports.help = {
  name: 'nick',
  description: 'Kullanılan sunucudaki Botun nick(Takma ad)ını değiştirir.',
  usage: 'nick <nick>'
};