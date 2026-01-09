# Daaglikse-krag
'n Toepassing vir mammas om deur God se woord krag te kry vir elke dag, wat 'n gebed, gedagte, skriflesing en vraag insluit. Met plek vir notas. Kan die gebed en skrif gedeelte ook deel met iemand wat jy voel dit dalk sal nodig kry. 
import React, { useState, useEffect } from 'react';
import { Heart, BookOpen, MessageCircle, Sparkles, Share2, Lock, Unlock, Settings, Send, NotebookPen } from 'lucide-react';

const AfrikaansMotherhoodApp = () => {
  const [currentDate] = useState(new Date());
  const [isLocked, setIsLocked] = useState(false);
  const [password, setPassword] = useState('');
  const [storedPassword, setStoredPassword] = useState('');
  const [inputPassword, setInputPassword] = useState('');
  const [showSettings, setShowSettings] = useState(false);
  const [passwordEnabled, setPasswordEnabled] = useState(false);
  const [showFeedback, setShowFeedback] = useState(false);
  const [feedbackText, setFeedbackText] = useState('');
  const [reflectionAnswer, setReflectionAnswer] = useState('');
  const [prayerNotes, setPrayerNotes] = useState('');
  const [showPrayerNotes, setShowPrayerNotes] = useState(false);
  
  useEffect(() => {
    const saved = localStorage.getItem('daaglikseKragData');
    if (saved) {
      const data = JSON.parse(saved);
      setStoredPassword(data.password || '');
      setPasswordEnabled(data.passwordEnabled || false);
      setIsLocked(data.passwordEnabled || false);
      setReflectionAnswer(data.reflectionAnswer || '');
      setPrayerNotes(data.prayerNotes || '');
    }
  }, []);
  
  const saveData = (updates) => {
    const saved = localStorage.getItem('daaglikseKragData');
    const data = saved ? JSON.parse(saved) : {};
    const newData = { ...data, ...updates };
    localStorage.setItem('daaglikseKragData', JSON.stringify(newData));
  };
  
  const dailyContent = [
    {
      verse: "Prediker 3:1",
      verseText: "Alles het sy bepaalde tyd, en daar is 'n tyd vir elke saak onder die hemel.",
      thought: "Of jy werk of tuis bly, daar is 'n seisoen vir alles. Jou keuse is nie 'n mislukking nie - dit is 'n seisoen. God het jou hier, nou, presies waar jy moet wees. Die spanning wat jy voel is eg, maar jou keuse is geldig.",
      question: "Watter seisoen is jy in? Kan jy jouself genade gee vir hierdie seisoen se uitdagings?",
      prayer: "Vader, help my om te aanvaar dat my keuse nie perfek hoef te wees nie. Gee my vrede in hierdie seisoen, of ek werk of tuis is. Laat my ophou om myself met ander te vergelyk. Amen."
    },
    {
      verse: "Jesaja 49:15",
      verseText: "Kan 'n vrou haar suigeling vergeet, sonder medelye wees met die seun van haar skoot? Al sou húlle vergeet, nogtans sal Ék jou nie vergeet nie!",
      thought: "Die skuld wat jy voel - of jy by die werk sit en aan jou kinders dink, of tuis is en voel asof jy jouself verloor - God verstaan. Hy vergeet jou nie. Jy is 'n goeie ma, selfs wanneer dit nie so voel nie.",
      question: "Watter gedeelte van jou moederskap laat jou die meeste skuldig voel? Kan jy dit vandag aan God gee?",
      prayer: "Here, die skuld is swaar. Help my om te onthou dat U my nie veroordeel nie. Ek doen my bes in moeilike omstandighede. Gee my genade vir myself. Amen."
    },
    {
      verse: "Filippense 4:6-7",
      verseText: "Wees oor niks besorg nie, maar laat julle begeertes in alles deur gebed en smeking met danksegging bekend word by God. En die vrede van God, wat alle verstand te bowe gaan, sal julle harte en julle sinne bewaar in Christus Jesus.",
      thought: "Die angs oor of jy die regte keuse gemaak het, vreet aan jou. Werk ek te veel? Moet ek tuis wees? Is ek genoeg? Bring al hierdie vrae na God. Hy belowe vrede wat verstand te bowe gaan.",
      question: "Watter spesifieke bekommernis oor jou werk-huis balans kan jy vandag in gebed aan God gee?",
      prayer: "Vader, my gedagtes is besig en bekommerd. Ek weet nie of ek die regte keuse gemaak het nie. Gee my U vrede wat my verstand nie kan verstaan nie. Stil my hart. Amen."
    },
    {
      verse: "Matteus 6:34",
      verseText: "Moenie dan besorg wees oor môre nie, want môre sal vir sy eie dinge besorg wees. Elke dag het genoeg aan sy eie kwaad.",
      thought: "Vandag het jy genoeg om mee te handel - die werksvergadering, die luiers, die aandete, die moegheid. Moenie ook nog môre se besluite vandag probeer maak nie. Een dag op 'n slag.",
      question: "Watter besluit oor die toekoms probeer jy vandag maak wat eintlik kan wag?",
      prayer: "Jesus, help my om net vandag te leef. Ek kan nie ook nog besluit oor môre nie. Gee my krag vir vandag se uitdagings. Môre sal vir homself sorg. Amen."
    },
    {
      verse: "2 Korintiërs 12:9",
      verseText: "Maar Hy het vir my gesê: My genade is vir jou genoeg, want my krag word in swakheid volbring.",
      thought: "Jy voel soms of jy in twee rigtings geskeur word. Die werksmom wat haar kinders mis. Die tuisma wat haar identiteit mis. Jou swakheid is presies waar God Se krag werk.",
      question: "In watter area voel jy vandag die swakste? Hoe kan God se krag daar werk?",
      prayer: "Here, ek voel swak en ontoereikend. Ek kan nie alles wees vir almal nie. Maar U sê U genade is genoeg. Laat my dit glo. Werk U krag in my swakheid uit. Amen."
    },
    {
      verse: "Spreuke 31:17",
      verseText: "Sy omgord haar heupe met krag en versterk haar arms.",
      thought: "Die Spreuke 31-vrou - sy werk, sy sorg, sy balanseer. Maar let op: sy omgord haar met krag. Dit kom nie outomaties nie. Jy moet doelbewus krag soek vir hierdie taak. Dit is reg om moeg te wees.",
      question: "Waar kan jy vandag krag vind? 'n Oomblik alleen? 'n Gesprek met 'n vriendin? Tyd met God?",
      prayer: "Vader, ek het krag nodig wat ek nie uit myself het nie. Help my om doelbewus te stop en by U krag te tap. Wys my waar om vandag vernuwing te vind. Amen."
    },
    {
      verse: "Psalm 46:5",
      verseText: "God is in haar binneste, sy sal nie wankel nie; God sal haar help as die môre aanbreek.",
      thought: "Elke môre breek aan met nuwe besluite: gaan ek werk toe met 'n swaar hart, of bly ek tuis en wonder of ek genoeg is? God is in jou binneste. Jy sal nie wankel nie. Hierdie seisoen sal verbygaan.",
      question: "Watter vrees kom elke môre saam met jou op? Hoe kan God jou help om dit te hanteer?",
      prayer: "Here, elke nuwe dag bring nuwe uitdagings. Help my om op te staan en te weet U is met my. Ek hoef nie alles uit te sorteer nie. U sal my help as môre aanbreek. Amen."
    }
  ];

  const getDayOfYear = (date) => {
    const start = new Date(date.getFullYear(), 0, 0);
    const diff = date - start;
    const oneDay = 1000 * 60 * 60 * 24;
    return Math.floor(diff / oneDay);
  };

  const dayIndex = getDayOfYear(currentDate) % dailyContent.length;
  const today = dailyContent[dayIndex];

  const handleLogin = () => {
    if (inputPassword === storedPassword) {
      setIsLocked(false);
      setInputPassword('');
    } else {
      alert('Verkeerde wagwoord!');
    }
  };

  const handleSetPassword = () => {
    if (password.length >= 4) {
      setStoredPassword(password);
      setPasswordEnabled(true);
      saveData({ password, passwordEnabled: true });
      setPassword('');
      setShowSettings(false);
      alert('Wagwoord gestel!');
    } else {
      alert('Wagwoord moet ten minste 4 karakters lank wees.');
    }
  };

  const handleDisablePassword = () => {
    setStoredPassword('');
    setPasswordEnabled(false);
    setIsLocked(false);
    saveData({ password: '', passwordEnabled: false });
    alert('Wagwoord verwyder!');
  };

  const handleSendFeedback = () => {
    if (feedbackText.trim()) {
      alert('Dankie vir jou terugvoer! Dit help ons om die app beter te maak. ❤️');
      setFeedbackText('');
      setShowFeedback(false);
    }
  };

  const handleSaveReflection = () => {
    saveData({ reflectionAnswer });
    alert('Jou antwoord is gestoor! ✨');
  };

  const handleSavePrayerNotes = () => {
    saveData({ prayerNotes });
    alert('Jou gebedsnota is gestoor! 🙏');
  };

  const shareVerse = async () => {
    await shareAsImage('verse', today.verse, today.verseText);
  };

  const sharePrayer = async () => {
    await shareAsImage('prayer', 'Gebed', today.prayer);
  };

  const shareAsImage = async (type, title, content) => {
    try {
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');
      
      if (!ctx) return;
      
      canvas.width = 1080;
      canvas.height = 1080;
      
      const gradient = ctx.createLinearGradient(0, 0, canvas.width, canvas.height);
      if (type === 'verse') {
        gradient.addColorStop(0, '#fef3c7');
        gradient.addColorStop(0.5, '#fef9e7');
        gradient.addColorStop(1, '#ffedd5');
      } else {
        gradient.addColorStop(0, '#fce7f3');
        gradient.addColorStop(1, '#fbcfe8');
      }
      ctx.fillStyle = gradient;
      ctx.fillRect(0, 0, canvas.width, canvas.height);
      
      ctx.fillStyle = 'rgba(134, 239, 172, 0.15)';
      ctx.beginPath();
      ctx.arc(900, 200, 150, 0, Math.PI * 2);
      ctx.fill();
      
      ctx.fillStyle = 'rgba(251, 113, 133, 0.15)';
      ctx.beginPath();
      ctx.arc(200, 850, 120, 0, Math.PI * 2);
      ctx.fill();
      
      ctx.fillStyle = 'rgba(134, 239, 172, 0.12)';
      ctx.beginPath();
      ctx.arc(100, 300, 80, 0, Math.PI * 2);
      ctx.fill();
      
      ctx.fillStyle = type === 'verse' ? '#047857' : '#be185d';
      ctx.font = 'bold 48px Georgia, serif';
      ctx.textAlign = 'center';
      ctx.fillText(title, canvas.width / 2, 150);
      
      ctx.fillStyle = '#374151';
      ctx.font = '36px Georgia, serif';
      ctx.textAlign = 'center';
      
      const maxWidth = 900;
      const lineHeight = 55;
      const words = content.split(' ');
      let line = '';
      let y = 350;
      
      for (let word of words) {
        const testLine = line + word + ' ';
        const metrics = ctx.measureText(testLine);
        
        if (metrics.width > maxWidth && line !== '') {
          ctx.fillText(line, canvas.width / 2, y);
          line = word + ' ';
          y += lineHeight;
        } else {
          line = testLine;
        }
      }
      ctx.fillText(line, canvas.width / 2, y);
      
      ctx.font = 'italic 28px Georgia, serif';
      ctx.fillStyle = '#6b7280';
      ctx.fillText('- Daaglikse Krag vir Moeders', canvas.width / 2, canvas.height - 100);
      
      canvas.toBlob(async (blob) => {
        if (!blob) return;
        
        const file = new File([blob], `${type}.png`, { type: 'image/png' });
        
        if (navigator.share && navigator.canShare && navigator.canShare({ files: [file] })) {
          try {
            await navigator.share({
              files: [file],
              title: type === 'verse' ? 'Dagvers' : 'Gebed',
            });
          } catch (err) {
            if (err.name !== 'AbortError') {
              downloadImage(canvas, type);
            }
          }
        } else {
          downloadImage(canvas, type);
        }
      });
    } catch (error) {
      console.error('Error sharing image:', error);
      alert('Kon nie deel nie. Probeer asseblief weer.');
    }
  };

  const downloadImage = (canvas, type) => {
    const link = document.createElement('a');
    link.download = `${type}-${new Date().toISOString().split('T')[0]}.png`;
    link.href = canvas.toDataURL();
    link.click();
  };

  const copyToClipboard = (text) => {
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(text).then(() => {
        alert('Gekopieër na knipbord!');
      }).catch(() => {
        alert('Kon nie kopieer nie. Probeer asseblief weer.');
      });
    } else {
      alert('Kon nie kopieer nie. Probeer asseblief weer.');
    }
  };

  if (isLocked && passwordEnabled) {
    return (
      <div className="min-h-screen bg-gradient-to-br from-green-50 via-rose-50 to-emerald-50 flex items-center justify-center p-6" style={{ fontFamily: 'Georgia, serif' }}>
        <div className="bg-white rounded-2xl shadow-2xl p-8 max-w-md w-full">
          <div className="text-center mb-6">
            <Lock className="w-16 h-16 text-rose-400 mx-auto mb-4" />
            <h2 className="text-2xl font-serif text-gray-800">Daaglikse Krag</h2>
            <p className="text-gray-600 mt-2">Tik jou wagwoord in</p>
          </div>
          <input
            type="password"
            value={inputPassword}
            onChange={(e) => setInputPassword(e.target.value)}
            onKeyPress={(e) => e.key === 'Enter' && handleLogin()}
            className="w-full px-4 py-3 border-2 border-gray-300 rounded-lg mb-4 focus:outline-none focus:border-rose-400"
            placeholder="Wagwoord"
          />
          <button
            onClick={handleLogin}
            className="w-full bg-rose-400 hover:bg-rose-500 text-white py-3 rounded-lg font-medium transition-colors"
          >
            Maak Oop
          </button>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gradient-to-br from-green-50 via-rose-50 to-emerald-50 relative overflow-hidden" style={{ fontFamily: 'Georgia, serif' }}>
      <div className="absolute top-8 left-8 opacity-30 animate-sway">
        <svg width="120" height="120" viewBox="0 0 120 120">
          <g transform="translate(60,60)">
            <ellipse cx="0" cy="0" rx="25" ry="35" fill="#86efac" opacity="0.6" transform="rotate(-30)"/>
            <ellipse cx="0" cy="0" rx="25" ry="35" fill="#86efac" opacity="0.6" transform="rotate(30)"/>
            <ellipse cx="0" cy="0" rx="25" ry="35" fill="#86efac" opacity="0.7"/>
            <path d="M 0 15 Q 5 40, 0 60" stroke="#15803d" strokeWidth="3" fill="none"/>
          </g>
        </svg>
      </div>
      
      <div className="absolute top-32 right-12 opacity-35 animate-float">
        <svg width="100" height="100" viewBox="0 0 100 100">
          <g transform="translate(50,50)">
            <circle cx="0" cy="0" r="8" fill="#fcd34d"/>
            <ellipse cx="0" cy="-20" rx="12" ry="18" fill="#fb7185" opacity="0.8"/>
            <ellipse cx="17" cy="-10" rx="12" ry="18" fill="#fb7185" opacity="0.8" transform="rotate(72)"/>
            <ellipse cx="11" cy="16" rx="12" ry="18" fill="#fb7185" opacity="0.8" transform="rotate(144)"/>
            <ellipse cx="-11" cy="16" rx="12" ry="18" fill="#fb7185" opacity="0.8" transform="rotate(216)"/>
            <ellipse cx="-17" cy="-10" rx="12" ry="18" fill="#fb7185" opacity="0.8" transform="rotate(288)"/>
          </g>
        </svg>
      </div>
      
      <div className="absolute bottom-24 left-16 opacity-25 animate-sway-slow">
        <svg width="140" height="140" viewBox="0 0 140 140">
          <g transform="translate(70,70)">
            <circle cx="0" cy="0" r="10" fill="#fef08a"/>
            <ellipse cx="0" cy="-25" rx="14" ry="22" fill="#fda4af" opacity="0.9"/>
            <ellipse cx="22" cy="-12" rx="14" ry="22" fill="#fda4af" opacity="0.9" transform="rotate(72)"/>
            <ellipse cx="14" cy="20" rx="14" ry="22" fill="#fda4af" opacity="0.9" transform="rotate(144)"/>
            <ellipse cx="-14" cy="20" rx="14" ry="22" fill="#fda4af" opacity="0.9" transform="rotate(216)"/>
            <ellipse cx="-22" cy="-12" rx="14" ry="22" fill="#fda4af" opacity="0.9" transform="rotate(288)"/>
          </g>
        </svg>
      </div>
      
      <div className="absolute bottom-16 right-8 opacity-30 animate-float-slow">
        <svg width="160" height="160" viewBox="0 0 160 160">
          <g transform="translate(80,80)">
            <ellipse cx="0" cy="0" rx="30" ry="40" fill="#6ee7b7" opacity="0.5" transform="rotate(-45)"/>
            <ellipse cx="0" cy="0" rx="30" ry="40" fill="#6ee7b7" opacity="0.5" transform="rotate(0)"/>
            <ellipse cx="0" cy="0" rx="30" ry="40" fill="#6ee7b7" opacity="0.6" transform="rotate(45)"/>
            <path d="M 0 20 Q 8 50, 0 80 T 0 120" stroke="#047857" strokeWidth="4" fill="none"/>
          </g>
        </svg>
      </div>
      
      <div className="absolute top-1/2 left-4 opacity-20 animate-sway">
        <svg width="80" height="80" viewBox="0 0 80 80">
          <g transform="translate(40,40)">
            <circle cx="0" cy="0" r="6" fill="#fde047"/>
            <ellipse cx="0" cy="-15" rx="10" ry="14" fill="#f472b6" opacity="0.8"/>
            <ellipse cx="13" cy="-7" rx="10" ry="14" fill="#f472b6" opacity="0.8" transform="rotate(72)"/>
            <ellipse cx="8" cy="12" rx="10" ry="14" fill="#f472b6" opacity="0.8" transform="rotate(144)"/>
            <ellipse cx="-8" cy="12" rx="10" ry="14" fill="#f472b6" opacity="0.8" transform="rotate(216)"/>
            <ellipse cx="-13" cy="-7" rx="10" ry="14" fill="#f472b6" opacity="0.8" transform="rotate(288)"/>
          </g>
        </svg>
      </div>
      
      <div className="absolute top-1/3 right-6 opacity-25 animate-float">
        <svg width="100" height="100" viewBox="0 0 100 100">
          <g transform="translate(50,50)">
            <ellipse cx="0" cy="0" rx="20" ry="28" fill="#86efac" opacity="0.6" transform="rotate(-25)"/>
            <ellipse cx="0" cy="0" rx="20" ry="28" fill="#86efac" opacity="0.6" transform="rotate(25)"/>
            <ellipse cx="0" cy="0" rx="20" ry="28" fill="#86efac" opacity="0.7" transform="rotate(0)"/>
            <path d="M 0 12 Q 6 35, 0 55" stroke="#166534" strokeWidth="3" fill="none"/>
          </g>
        </svg>
      </div>
      
      <style>{`
        @keyframes sway {
          0%, 100% { transform: rotate(-3deg); }
          50% { transform: rotate(3deg); }
        }
        @keyframes sway-slow {
          0%, 100% { transform: rotate(-2deg); }
          50% { transform: rotate(2deg); }
        }
        @keyframes float {
          0%, 100% { transform: translateY(0px); }
          50% { transform: translateY(-10px); }
        }
        @keyframes float-slow {
          0%, 100% { transform: translateY(0px); }
          50% { transform: translateY(-15px); }
        }
        .animate-sway {
          animation: sway 4s ease-in-out infinite;
        }
        .animate-sway-slow {
          animation: sway-slow 5s ease-in-out infinite;
        }
        .animate-float {
          animation: float 3s ease-in-out infinite;
        }
        .animate-float-slow {
          animation: float-slow 4s ease-in-out infinite;
        }
      `}</style>
      
      <div className="max-w-2xl mx-auto p-6 space-y-6 relative z-10">
        
        <div className="flex justify-between items-start">
          <div className="text-center flex-1 py-8">
            <div className="flex items-center justify-center gap-2 mb-3">
              <Heart className="w-8 h-8 text-rose-400" />
              <h1 className="text-3xl font-serif text-gray-800">Daaglikse Krag</h1>
            </div>
            <p className="text-rose-500 font-medium">vir Moeders</p>
            <p className="text-sm text-gray-600 mt-2">
              {currentDate.toLocaleDateString('af-ZA', { 
                weekday: 'long', 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
              })}
            </p>
          </div>
          <button
            onClick={() => setShowSettings(!showSettings)}
            className="bg-white p-3 rounded-full shadow-lg hover:shadow-xl transition-shadow"
          >
            <Settings className="w-5 h-5 text-gray-600" />
          </button>
        </div>

        {showSettings && (
          <div className="bg-white rounded-2xl shadow-lg p-6">
            <h3 className="text-lg font-semibold text-gray-800 mb-4">Instellings</h3>
            
            <div className="space-y-4">
              <div>
                <label className="block text-sm font-medium text-gray-700 mb-2">
                  {passwordEnabled ? 'Verander Wagwoord' : 'Stel Wagwoord'}
                </label>
                <input
                  type="password"
                  value={password}
                  onChange={(e) => setPassword(e.target.value)}
                  className="w-full px-4 py-2 border-2 border-gray-300 rounded-lg mb-2 focus:outline-none focus:border-rose-400"
                  placeholder="Nuwe wagwoord (min. 4 karakters)"
                />
                <button
                  onClick={handleSetPassword}
                  className="w-full bg-emerald-500 hover:bg-emerald-600 text-white py-2 rounded-lg font-medium transition-colors"
                >
                  Stoor Wagwoord
                </button>
              </div>
              
              {passwordEnabled && (
                <button
                  onClick={handleDisablePassword}
                  className="w-full bg-gray-500 hover:bg-gray-600 text-white py-2 rounded-lg font-medium transition-colors"
                >
                  <Unlock className="w-4 h-4 inline mr-2" />
                  Verwyder Wagwoord
                </button>
              )}
            </div>
          </div>
        )}

        <div className="bg-gradient-to-br from-amber-50 via-yellow-50 to-orange-50 rounded-2xl shadow-lg p-8 border-t-4 border-emerald-400 relative overflow-hidden">
          <div className="absolute top-3 right-3 opacity-20">
            <svg width="60" height="60" viewBox="0 0 60 60">
              <g transform="translate(30,30)">
                <circle cx="0" cy="0" r="4" fill="#fcd34d"/>
                <ellipse cx="0" cy="-10" rx="6" ry="9" fill="#fb7185" opacity="0.8"/>
                <ellipse cx="8.5" cy="-5" rx="6" ry="9" fill="#fb7185" opacity="0.8" transform="rotate(72)"/>
                <ellipse cx="5.5" cy="8" rx="6" ry="9" fill="#fb7185" opacity="0.8" transform="rotate(144)"/>
                <ellipse cx="-5.5" cy="8" rx="6" ry="9" fill="#fb7185" opacity="0.8" transform="rotate(216)"/>
                <ellipse cx="-8.5" cy="-5" rx="6" ry="9" fill="#fb7185" opacity="0.8" transform="rotate(288)"/>
              </g>
            </svg>
          </div>
          <div className="absolute bottom-3 left-3 opacity-20">
            <svg width="50" height="50" viewBox="0 0 50 50">
              <g transform="translate(25,25)">
                <ellipse cx="0" cy="0" rx="12" ry="17" fill="#86efac" opacity="0.7"/>
                <path d="M 0 8 Q 3 20, 0 30" stroke="#15803d" strokeWidth="2" fill="none"/>
              </g>
            </svg>
          </div>
          
          <div className="flex items-center justify-between mb-4 relative z-10">
            <div className="flex items-center gap-2">
              <BookOpen className="w-5 h-5 text-emerald-600" />
              <h2 className="text-xl font-semibold text-gray-800">Dagvers</h2>
            </div>
            <button 
              onClick={shareVerse}
              className="flex items-center gap-1 px-3 py-2 bg-emerald-100 hover:bg-emerald-200 text-emerald-700 rounded-lg transition-colors"
            >
              <Share2 className="w-4 h-4" />
              <span className="text-sm">Deel</span>
            </button>
          </div>
          <p className="text-sm text-emerald-700 font-medium mb-2 relative z-10">{today.verse}</p>
          <p className="text-gray-700 italic leading-relaxed text-lg relative z-10">{today.verseText}</p>
        </div>

        <div className="bg-white rounded-2xl shadow-lg p-6 relative overflow-hidden">
          <div className="absolute top-3 right-3 opacity-15">
            <svg width="50" height="50" viewBox="0 0 50 50">
              <g transform="translate(25,25)">
                <circle cx="0" cy="0" r="3" fill="#fde047"/>
                <ellipse cx="0" cy="-8" rx="5" ry="7" fill="#f472b6" opacity="0.8"/>
                <ellipse cx="7" cy="-4" rx="5" ry="7" fill="#f472b6" opacity="0.8" transform="rotate(72)"/>
                <ellipse cx="4" cy="6" rx="5" ry="7" fill="#f472b6" opacity="0.8" transform="rotate(144)"/>
                <ellipse cx="-4" cy="6" rx="5" ry="7" fill="#f472b6" opacity="0.8" transform="rotate(216)"/>
                <ellipse cx="-7" cy="-4" rx="5" ry="7" fill="#f472b6" opacity="0.8" transform="rotate(288)"/>
              </g>
            </svg>
          </div>
          <div className="flex items-center gap-2 mb-4 relative z-10">
            <Sparkles className="w-5 h-5 text-rose-500" />
            <h2 className="text-xl font-semibold text-gray-800">Gedagte vir Vandag</h2>
          </div>
          <p className="text-gray-700 leading-relaxed relative z-10">{today.thought}</p>
        </div>

        <div className="bg-gradient-to-br from-emerald-50 to-green-100 rounded-2xl shadow-lg p-6 relative overflow-hidden">
          <div className="absolute bottom-2 right-2 opacity-20">
            <svg width="70" height="70" viewBox="0 0 70 70">
              <g transform="translate(35,35)">
                <ellipse cx="0" cy="0" rx="15" ry="20" fill="#86efac" opacity="0.7" transform="rotate(-20)"/>
                <ellipse cx="0" cy="0" rx="15" ry="20" fill="#86efac" opacity="0.6" transform="rotate(20)"/>
                <path d="M 0 10 Q 4 25, 0 40" stroke="#166534" strokeWidth="2" fill="none"/>
              </g>
            </svg>
          </div>
          <div className="flex items-center gap-2 mb-4 relative z-10">
            <MessageCircle className="w-5 h-5 text-emerald-700" />
            <h2 className="text-xl font-semibold text-gray-800">Besinning</h2>
          </div>
          <p className="text-gray-700 leading-relaxed relative z-10 mb-4">{today.question}</p>
          
          <div className="relative z-10">
            <label className="block text-sm font-medium text-gray-700 mb-2">Jou Antwoord:</label>
            <textarea
              value={reflectionAnswer}
              onChange={(e) => setReflectionAnswer(e.target.value)}
              className="w-full px-4 py-3 border-2 border-emerald-200 rounded-lg focus:outline-none focus:border-emerald-400 min-h-24"
              placeholder="Tik hier as jy wil reflekteer..."
            />
            <button
              onClick={handleSaveReflection}
              className="mt-2 bg-emerald-500 hover:bg-emerald-600 text-white px-4 py-2 rounded-lg font-medium transition-colors"
            >
              Stoor Antwoord
            </button>
          </div>
        </div>

        <div className="bg-gradient-to-br from-rose-50 to-pink-100 rounded-2xl shadow-lg p-6 relative overflow-hidden">
          <div className="absolute top-3 left-3 opacity-20">
            <svg width="60" height="60" viewBox="0 0 60 60">
              <g transform="translate(30,30)">
                <circle cx="0" cy="0" r="4" fill="#fef08a"/>
                <ellipse cx="0" cy="-11" rx="7" ry="10" fill="#fda4af" opacity="0.9"/>
                <ellipse cx="9.5" cy="-5.5" rx="7" ry="10" fill="#fda4af" opacity="0.9" transform="rotate(72)"/>
                <ellipse cx="6" cy="9" rx="7" ry="10" fill="#fda4af" opacity="0.9" transform="rotate(144)"/>
                <ellipse cx="-6" cy="9" rx="7" ry="10" fill="#fda4af" opacity="0.9" transform="rotate(216)"/>
                <ellipse cx="-9.5" cy="-5.5" rx="7" ry="10" fill="#fda4af" opacity="0.9" transform="rotate(288)"/>
              </g>
            </svg>
          </div>
          <div className="absolute bottom-3 right-3 opacity-15">
            <svg width="50" height="50" viewBox="0 0 50 50">
              <g transform="translate(25,25)">
                <circle cx="0" cy="0" r="3" fill="#fef08a"/>
                <ellipse cx="0" cy="-9" rx="6" ry="8" fill="#fb7185" opacity="0.9"/>
                <ellipse cx="8" cy="-4.5" rx="6" ry="8" fill="#fb7185" opacity="0.9" transform="rotate(72)"/>
                <ellipse cx="5" cy="7.5" rx="6" ry="8" fill="#fb7185" opacity="0.9" transform="rotate(144)"/>
                <ellipse cx="-5" cy="7.5" rx="6" ry="8" fill="#fb7185" opacity="0.9" transform="rotate(216)"/>
                <ellipse cx="-8" cy="-4.5" rx="6" ry="8" fill="#fb7185" opacity="0.9" transform="rotate(288)"/>
              </g>
            </svg>
          </div>
          <div className="flex items-center justify-between mb-4 relative z-10">
            <div className="flex items-center gap-2">
              <Heart className="w-5 h-5 text-rose-500" />
              <h2 className="text-xl font-semibold text-gray-800">Gebed</h2>
            </div>
            <button 
              onClick={sharePrayer}
              className="flex items-center gap-1 px-3 py-2 bg-rose-100 hover:bg-rose-200 text-rose-700 rounded-lg transition-colors"
            >
              <Share2 className="w-4 h-4" />
              <span className="text-sm">Deel</span>
            </button>
          </div>
          <p className="text-gray-700 leading-relaxed italic relative z-10">{today.prayer}</p>
        </div>

        <div className="bg-white rounded-2xl shadow-lg p-6">
          <button
            onClick={() => setShowPrayerNotes(!showPrayerNotes)}
            className="flex items-center gap-2 w-full text-left mb-4"
          >
            <NotebookPen className="w-5 h-5 text-purple-500" />
            <h2 className="text-xl font-semibold text-gray-800">Gebedsnota</h2>
          </button>
          
          {showPrayerNotes && (
            <div>
              <p className="text-sm text-gray-600 mb-3">Skryf jou persoonlike gebede en gedagtes hier neer:</p>
              <textarea
                value={prayerNotes}
                onChange={(e) => setPrayerNotes(e.target.value)}
                className="w-full px-4 py-3 border-2 border-purple-200 rounded-lg focus:outline-none focus:border-purple-400 min-h-32"
                placeholder="Wat wil jy vandag aan God gee? Waarvoor bid jy?"
              />
              <button
                onClick={handleSavePrayerNotes}
                className="mt-2 bg-purple-500 hover:bg-purple-600 text-white px-4 py-2 rounded-lg font-medium transition-colors"
              >
                Stoor Nota
              </button>
            </div>
          )}
        </div>

        <div className="text-center">
          <button
            onClick={() => setShowFeedback(!showFeedback)}
            className="bg-white hover:bg-gray-50 text-gray-700 px-6 py-3 rounded-lg shadow-lg font-medium transition-colors inline-flex items-center gap-2"
          >
            <Send className="w-4 h-4" />
            Terugvoer & Voorstelle
          </button>
        </div>

        {showFeedback && (
          <div className="bg-white rounded-2xl shadow-lg p-6">
            <h3 className="text-lg font-semibold text-gray-800 mb-3">Deel jou gedagtes met ons</h3>
            <p className="text-sm text-gray-600 mb-4">
              Ons wil graag hoor hoe ons die app beter kan maak vir jou! ❤️
            </p>
            <textarea
              value={feedbackText}
              onChange={(e) => setFeedbackText(e.target.value)}
              className="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:outline-none focus:border-rose-400 min-h-32"
              placeholder="Skryf jou terugvoer, klagtes, of voorstelle hier..."
            />
            <button
              onClick={handleSendFeedback}
              className="mt-3 bg-rose-400 hover:bg-rose-500 text-white px-6 py-2 rounded-lg font-medium transition-colors"
            >
              Stuur
            </button>
          </div>
        )}

        <div className="text-center py-6">
          <p className="text-sm text-gray-600">
            Jy doen 'n wonderlike werk, Ma. ❤️
          </p>
          <p className="text-xs text-gray-500 mt-2">
            God sien jou en seën jou.
          </p>
        </div>

      </div>
    </div>
  );
};

export default AfrikaansMotherhoodApp;
