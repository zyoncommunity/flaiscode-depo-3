const db = require('quick.db')
const Discord = require('discord.js')

exports.run = async (bot, message, args) => {
  if (!args[0]) return message.channel.send('aç yada kapat yazmalısın! Örnek: küfür-engel aç')
  if (!message.member.hasPermission('MANAGE_GUILD')) return message.channel.send('`SUNUCUYU_YÖNET` yetkisine sahip olmalısın!')
  
  if (args[0] == 'aç') {
    db.set(`kufur_${message.guild.id}`, 'acik').then(i => {
      message.channel.send('✅ Küfur Engel başarıyla açıldı! Üyeleri Yasakla yetkisine sahip olanların küfürü engellenmicektir.')
    })
  }
  if (args[0] == 'kapat') {
    db.set(`kufur_${message.guild.id}`, 'kapali').then(i => {
      message.channel.send('✅ Küfür Engel başarıyla kapatıldı! Artık herkes küfür yazabilir.')
    })
  }

}

exports.conf = {
  enabled: true,
  guildOnly: false,
  aliases: ['küfür'],
  permLevel: 0
};

exports.help = {
  name: 'küfür-engelleme',
  description: '[Admin Komutu]',
  usage: 'küfür-engelleme'
};

//bot.js

client.on("message", msg => {
  
  
  db.fetch(`kufur_${msg.guild.id}`).then(i => {
    if (i == 'acik') {
        const kufur = ["oç", "amk", "ananı sikiyim", "ananıskm", "piç", "amk", "amsk", "sikim", "sikiyim", "orospu çocuğu", "piç kurusu", "kahpe", "orospu", "mal", "sik", "yarrak", "am", "amcık", "amık", "yarram", "sikimi ye", "mk", "mq", "aq", "ak", "amq",];
        if (kufur.some(word => msg.content.includes(word))) {
          try {
            if (!msg.member.hasPermission("BAN_MEMBERS")) {
                  msg.delete();

                  return msg.reply('Küfür etmemelisin! ⚠').then(msg => msg.delete(3000));
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
 