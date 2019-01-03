const db = require('quick.db')
const Discord = require('discord.js')

exports.run = async (bot, message, args) => {
  if (!args[0]) return message.channel.send('aç yada kapat yazmalısın! Örnek: reklam-engel aç')
  if (!message.member.hasPermission('MANAGE_GUILD')) return message.channel.send('`SUNUCUYU_YÖNET` yetkisine sahip olmalısın!')
  
  if (args[0] == 'aç') {
    db.set(`reklam_${message.guild.id}`, 'acik').then(i => {
      message.channel.send('✅ Reklam Engel başarıyla açıldı! Üyeleri Yasakla yetkisine sahip olanlar`ın reklama engellenmicektir.')
    })
  }
  if (args[0] == 'kapat') {
    db.set(`reklam_${message.guild.id}`, 'kapali').then(i => {
      message.channel.send('✅ Reklam Engel başarıyla kapatıldı! Artık herkes reklam yapabilir.')
    })
  }

}

exports.conf = {
  enabled: true,
  guildOnly: false,
  aliases: ['reklam'],
  permLevel: 0
};

exports.help = {
  name: 'reklam-engelleme',
  description: '[Admin Komutu]',
  usage: 'reklam-engelleme'
};

//bot.js

client.on("message", msg => {
  
  
  db.fetch(`reklam_${msg.guild.id}`).then(i => {
    if (i == 'acik') {
        const reklam = [".com", ".net", ".xyz", ".tk", ".pw", ".io", ".me", ".gg", "www.", "https", "http", ".gl", ".org", ".com.tr", ".biz", "net", ".rf.gd", ".az", ".party",];
        if (reklam.some(word => msg.content.includes(word))) {
          try {
            if (!msg.member.hasPermission("BAN_MEMBERS")) {
                  msg.delete();

                  return msg.reply('Reklam yapmamalısın ⚠').then(msg => msg.delete(3000));
            }              
          } catch(err) {
            console.log(err);
          }
        }
    }
    else if (i == 'kapali') {
      
    }
    if (!i) return;
  })
    });
 