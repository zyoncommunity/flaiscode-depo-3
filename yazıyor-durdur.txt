const Discord = require('discord.js');

exports.run = (client, message, args) => {
  if ( message.react('🖤')) {
  message.channel.stopTyping();
  message.delete()
}

};

exports.help = {
  name: "yazıyordurdur",
  description: "deneme.",
  usage: "duyuru <mesajın>"
}

exports.conf = {
  enabled: true,
  guildOnly: true,
  permlevel: 0,
  aliases: ["yazıyor"]
}