import React, { useState, useEffect } from 'react';
import { 
  Heart, Sparkles, Compass, History, Settings, User, LogOut, 
  Play, CheckCircle, RotateCcw, Clock, Sun, Eye, EyeOff, ShieldCheck 
} from 'lucide-react';

// ==========================================
// 1. BANK DATA 30 CHALLENGE JEDA
// ==========================================
const INITIAL_CHALLENGES = [
  // Spiritualitas (10)
  { id: "sp-1", category: "Spiritualitas", title: "Istighfar dan Napas Sadar", instruction: "Berhenti sejenak dari layarmu. Tarik napas perlahan, dan ucapkan istighfar/doa permohonan ampun dengan penuh kesadaran dan keheningan hati.", durationMinutes: 2, hasReflection: false },
  { id: "sp-2", category: "Spiritualitas", title: "Satu Menit Zikir / Keheningan", instruction: "Luangkan 60 detik untuk berzikir atau hening menata hati tanpa menyentuh aplikasi lain atau merespons notifikasi.", durationMinutes: 1, hasReflection: false },
  { id: "sp-3", category: "Spiritualitas", title: "Refleksi Rasa Syukur", instruction: "Sebutkan atau tuliskan satu nikmat kecil yang kamu terima hari ini yang sering kali luput dari perhatianmu.", durationMinutes: 3, hasReflection: true, prompt: "Apa satu hal yang sangat kamu syukuri hari ini?" },
  { id: "sp-4", category: "Spiritualitas", title: "Menata Kembali Niat", instruction: "Ambil waktu sejenak untuk berdoa singkat. Luruskan kembali niat atas apa yang sedang kamu kerjakan hari ini.", durationMinutes: 2, hasReflection: true, prompt: "Apa niat utama yang ingin kamu jaga hari ini?" },
  { id: "sp-5", category: "Spiritualitas", title: "Rencana Kebaikan Kecil", instruction: "Renungkan satu tindakan kecil bernilai ibadah/kebaikan yang bisa kamu lakukan sebelum hari ini berakhir.", durationMinutes: 3, hasReflection: true, prompt: "Tindakan bermanfaat apa yang akan kamu lakukan hari ini?" },
  { id: "sp-6", category: "Spiritualitas", title: "Mengingat Kebesaran Semesta", instruction: "Tatap keluar jendela atau amati lingkungan sekitarmu selama 2 menit. Rasakan kedamaian dan kebesaran Pencipta.", durationMinutes: 2, hasReflection: false },
  { id: "sp-7", category: "Spiritualitas", title: "Doa untuk Orang Lain", instruction: "Kirimkan doa kebaikan secara diam-diam untuk teman, keluarga, atau seseorang yang sedang mengalami kesulitan.", durationMinutes: 2, hasReflection: true, prompt: "Siapa yang kamu doakan dan doa baik apa yang kamu panjatkan?" },
  { id: "sp-8", category: "Spiritualitas", title: "Melepas Beban dan Tawakal", instruction: "Identifikasi satu kecemasan yang di luar kendalimu, lalu bayangkan kamu menyerahkannya penuh pasrah kepada Tuhan.", durationMinutes: 4, hasReflection: true, prompt: "Kecemasan apa yang ingin kamu lepaskan hari ini?" },
  { id: "sp-9", category: "Spiritualitas", title: "Membaca Ayat / Kata Mutiara Hikmah", instruction: "Luangkan waktu sejenak membaca satu ayat kitab suci atau kata hikmah yang menyejukkan jiwamu.", durationMinutes: 3, hasReflection: false },
  { id: "sp-10", category: "Spiritualitas", title: "Evaluasi Diri Tanpa Menghakimi", instruction: "Hening sejenak dan evaluasi niat serta tindakanmu sepanjang hari ini dengan kasih sayang pada diri sendiri.", durationMinutes: 3, hasReflection: true, prompt: "Hal baik apa yang sudah kamu lakukan dan apa yang ingin diperbaiki?" },

  // Regulasi Emosi (10)
  { id: "re-1", category: "Regulasi Emosi", title: "Identifikasi Emosi Saat Ini", instruction: "Berhenti sebentar. Dengarkan tubuh dan pikiranmu. Emosi apa yang paling mendominasi perasaanmu saat ini?", durationMinutes: 2, hasReflection: true, prompt: "Apa emosi yang paling kamu rasakan saat ini?" },
  { id: "re-2", category: "Regulasi Emosi", title: "Pelacakan Pemicu Emosi", instruction: "Pikirkan hal atau konten apa yang memicu perasaan yang kamu alami sekarang.", durationMinutes: 3, hasReflection: true, prompt: "Apa yang membuatmu merasa demikian?" },
  { id: "re-3", category: "Regulasi Emosi", title: "Teknik Olah Napas 4-7-8", instruction: "Sebelum membuka media sosial lagi, tarik napas 4 detik, tahan 7 detik, dan hembuskan perlahan selama 8 detik. Ulangi 3 kali.", durationMinutes: 2, hasReflection: false },
  { id: "re-4", category: "Regulasi Emosi", title: "Evaluasi Dampak Konten Digital", instruction: "Ingat konten terakhir yang baru saja kamu lihat di layar.", durationMinutes: 2, hasReflection: true, prompt: "Apakah konten yang baru saja kamu lihat membuatmu lebih tenang atau justru lelah?" },
  { id: "re-5", category: "Regulasi Emosi", title: "Mencari Respons Sehat", instruction: "Jika ada hal yang mengganggu di media sosial, tentukan respons yang paling menjaga kedamaian pikiranmu.", durationMinutes: 3, hasReflection: true, prompt: "Apa respons yang lebih sehat yang bisa kamu pilih?" },
  { id: "re-6", category: "Regulasi Emosi", title: "Pesan Afeksi Diri", instruction: "Tuliskan satu kalimat yang hangat, lembut, dan menguatkan untuk dirimu sendiri yang sedang berjuang.", durationMinutes: 2, hasReflection: true, prompt: "Apa pesan hangat yang ingin kamu sampaikan pada dirimu sendiri?" },
  { id: "re-7", category: "Regulasi Emosi", title: "Pemeriksaan Ketegangan Tubuh", instruction: "Rasakan bahu, leher, dan rahangmu. Kendurkan otot yang tegang dan biarkan tubuhmu beristirahat sejenak.", durationMinutes: 2, hasReflection: false },
  { id: "re-8", category: "Regulasi Emosi", title: "Memisahkan Fakta vs Asumsi", instruction: "Jika ada kecemasan saat ini, pisahkan mana yang merupakan fakta nyata dan mana yang sekadar asumsi pikiran.", durationMinutes: 4, hasReflection: true, prompt: "Fakta apa yang menenangkan dari situasi yang kamu cemaskan?" },
  { id: "re-9", category: "Regulasi Emosi", title: "Grounding 5-4-3-2-1", instruction: "Sebutkan 5 benda yang kamu lihat, 4 hal yang dirasakan tubuh, 3 suara yang terdengar, 2 aroma, dan 1 rasa.", durationMinutes: 3, hasReflection: false },
  { id: "re-10", category: "Regulasi Emosi", title: "Jeda Konsumsi Informasi", instruction: "Putuskan untuk tidak mencari kabar atau konten berita baru selama 1 jam ke depan demi kesehatan emosimu.", durationMinutes: 1, hasReflection: true, prompt: "Apa yang akan kamu lakukan selama 1 jam tanpa linimasa berita?" },

  // Kebermaknaan Sosial dan Lingkungan (10)
  { id: "ks-1", category: "Kebermaknaan Sosial dan Lingkungan", title: "Aksi Kebaikan Sosial Hari Ini", instruction: "Renungkan atau lakukan satu tindakan nyata yang meringankan beban atau menyenangkan orang lain hari ini.", durationMinutes: 3, hasReflection: true, prompt: "Apa satu hal baik yang sudah atau akan kamu lakukan untuk orang lain hari ini?" },
  { id: "ks-2", category: "Kebermaknaan Sosial dan Lingkungan", title: "Koneksi Nyata Tanpa HP", instruction: "Ingat kembali momen interaksi sosial langsungmu hari ini tanpa distraksi ponsel di genggaman.", durationMinutes: 2, hasReflection: true, prompt: "Kapan terakhir kali kamu berbicara penuh hadir dengan keluarga/teman tanpa HP?" },
  { id: "ks-3", category: "Kebermaknaan Sosial dan Lingkungan", title: "Menyapa Rekan / Teman", instruction: "Cobalah menyapa atau mengirimkan pesan hangat penuh perhatian kepada seorang teman yang sudah lama tidak kamu kontak.", durationMinutes: 2, hasReflection: true, prompt: "Siapa yang kamu sapa dan bagaimana responsnya?" },
  { id: "ks-4", category: "Kebermaknaan Sosial dan Lingkungan", title: "Merapikan Ruang Fisik", instruction: "Letakkan ponselmu. Luangkan 5 menit penuh untuk merapikan meja belajar atau area di sekitarmu.", durationMinutes: 5, hasReflection: false },
  { id: "ks-5", category: "Kebermaknaan Sosial dan Lingkungan", title: "Mendengar Penuh Empati", instruction: "Niatkan untuk mendengarkan seseorang hari ini tanpa memotong pembicaraannya atau mengecek ponsel.", durationMinutes: 3, hasReflection: true, prompt: "Siapa seseorang yang membutuhkan pendengaran dan perhatianmu hari ini?" },
  { id: "ks-6", category: "Kebermaknaan Sosial dan Lingkungan", title: "Aksi Kecil Kepedulian Lingkungan", instruction: "Lakukan tindakan nyata untuk lingkungan sekitar: mematikan lampu yang tak dipakai, merawat tanaman, atau membuang sampah.", durationMinutes: 3, hasReflection: true, prompt: "Tindakan ramah lingkungan apa yang kamu lakukan hari ini?" },
  { id: "ks-7", category: "Kebermaknaan Sosial dan Lingkungan", title: "Hadir Sepenuhnya (Mindful Presence)", instruction: "Saat mengobrol nanti, letakkan ponsel di dalam tas/saku dan tatap mata lawan bicaramu dengan hangat.", durationMinutes: 2, hasReflection: false },
  { id: "ks-8", category: "Kebermaknaan Sosial dan Lingkungan", title: "Apresiasi Tenaga & Kerjasama", instruction: "Sampaikan ucapan terima kasih yang tulus kepada seseorang yang telah membantumu hari ini (petugas, teman, keluarga).", durationMinutes: 2, hasReflection: true, prompt: "Kepada siapa kamu mengucapkan terima kasih dan atas bantuan apa?" },
  { id: "ks-9", category: "Kebermaknaan Sosial dan Lingkungan", title: "Minum Air Tanpa Layar", instruction: "Ambil segelas air minum. Minumlah perlahan-lahan nikmati rasanya tanpa memegang ponsel sama sekali.", durationMinutes: 2, hasReflection: false },
  { id: "ks-10", category: "Kebermaknaan Sosial dan Lingkungan", title: "Jeda Jalan Kaki Singkat", instruction: "Berjalan kakilah sekitar ruangan atau luar rumah selama 3 menit tanpa membawa ponsel. Rasakan setiap langkahmu.", durationMinutes: 3, hasReflection: false }
];

// ==========================================
// 2. LOGIKA STORAGE & SESI MULTI-USER
// ==========================================
const USERS_KEY = "jeda_registered_users";
const CURRENT_USER_KEY = "jeda_current_user_session";

const getRegisteredUsers = () => {
  const users = localStorage.getItem(USERS_KEY);
  return users ? JSON.parse(users) : [];
};

const getUserStoreKey = (username, keyName) => `jeda_${username}_${keyName}`;

const initUserDataStore = (username, seedDemo = false) => {
  const checkInsKey = getUserStoreKey(username, "checkins");
  const historyKey = getUserStoreKey(username, "history");
  const affirmationsKey = getUserStoreKey(username, "affirmations");

  if (!localStorage.getItem(checkInsKey)) {
    const defaultCheckins = seedDemo ? [
      { id: 1, date: new Date(Date.now() - 86400000 * 2).toISOString(), emotion: "Lelah" },
      { id: 2, date: new Date(Date.now() - 86400000 * 1).toISOString(), emotion: "Cemas" },
      { id: 3, date: new Date().toISOString(), emotion: "Tenang" }
    ] : [];
    localStorage.setItem(checkInsKey, JSON.stringify(defaultCheckins));
  }

  if (!localStorage.getItem(historyKey)) {
    const defaultHistory = seedDemo ? [
      { id: "hist-1", challengeId: "re-1", title: "Identifikasi Emosi Saat Ini", category: "Regulasi Emosi", completedAt: new Date(Date.now() - 86400000 * 1).toISOString(), durationMinutes: 2, reflection: "Merasa sedikit lelah setelah membaca berita terbaru." },
      { id: "hist-2", challengeId: "sp-3", title: "Refleksi Rasa Syukur", category: "Spiritualitas", completedAt: new Date().toISOString(), durationMinutes: 3, reflection: "Bersyukur masih bisa menikmati kopi hangat pagi ini." }
    ] : [];
    localStorage.setItem(historyKey, JSON.stringify(defaultHistory));
  }

  if (!localStorage.getItem(affirmationsKey)) {
    const defaultAffirmations = seedDemo ? [
      { id: "aff-1", date: new Date().toISOString().split("T")[0], text: "Aku berhak menjalani hari ini dengan tenang dan penuh kesadaran tanpa terburu-buru oleh distraksi." }
    ] : [];
    localStorage.setItem(affirmationsKey, JSON.stringify(defaultAffirmations));
  }
};

const getUserData = (username, dataKey) => {
  const data = localStorage.getItem(getUserStoreKey(username, dataKey));
  return data ? JSON.parse(data) : [];
};

const saveUserData = (username, dataKey, value) => {
  localStorage.setItem(getUserStoreKey(username, dataKey), JSON.stringify(value));
};

const clearUserData = (username) => {
  localStorage.removeItem(getUserStoreKey(username, "checkins"));
  localStorage.removeItem(getUserStoreKey(username, "history"));
  localStorage.removeItem(getUserStoreKey(username, "affirmations"));
};

// ==========================================
// 3. KOMPONEN UTAMA APLIKASI
// ==========================================
export default function App() {
  const [currentUser, setCurrentUser] = useState(null);
  const [authTab, setAuthTab] = useState('welcome'); // 'welcome', 'login', 'register', 'onboarding'
  const [activeTab, setActiveTab] = useState('dashboard'); // 'dashboard', 'challenge', 'morning', 'history', 'settings', 'profile'
  
  // Auth Form State
  const [formData, setFormData] = useState({ fullName: '', username: '', email: '', password: '', confirmPassword: '', agreeTerms: false });
  const [showPassword, setShowPassword] = useState(false);
  const [authError, setAuthError] = useState('');
  const [resetSimulated, setResetSimulated] = useState(false);

  // Data Per-User State
  const [userPreferences, setUserPreferences] = useState({
    preferredCategories: ["Spiritualitas", "Regulasi Emosi", "Kebermaknaan Sosial dan Lingkungan"],
    reminderIntervalHours: 3,
    morningJedaTime: "06:00",
    monthlyTarget: 30,
    restrictedApps: ["Instagram", "TikTok", "X (Twitter)"]
  });
  const [checkIns, setCheckIns] = useState([]);
  const [history, setHistory] = useState([]);
  const [affirmations, setAffirmations] = useState([]);

  // Active Challenge State
  const [currentChallenge, setCurrentChallenge] = useState(null);
  const [reflectionInput, setReflectionInput] = useState('');
  const [selectedCategoryFilter, setSelectedCategoryFilter] = useState('Semua');
  const [morningText, setMorningText] = useState('');

  // Check Session On Load
  useEffect(() => {
    const session = localStorage.getItem(CURRENT_USER_KEY);
    if (session) {
      const parsed = JSON.parse(session);
      setCurrentUser(parsed);
      loadUserData(parsed);
    }
  }, []);

  const loadUserData = (user) => {
    if (user.preferences) setUserPreferences(user.preferences);
    setCheckIns(getUserData(user.username, 'checkins'));
    setHistory(getUserData(user.username, 'history'));
    setAffirmations(getUserData(user.username, 'affirmations'));
  };

  // Handlers
  const handleLoginSubmit = (e) => {
    e.preventDefault();
    setAuthError('');
    const inputKey = formData.username || formData.email;
    
    if (inputKey === 'demo' || inputKey === 'demo@jeda.id') {
      handleDemoLogin();
      return;
    }

    const users = getRegisteredUsers();
    const found = users.find(u => (u.email === inputKey || u.username === inputKey) && u.password === formData.password);

    if (found) {
      const sessionUser = { ...found };
      delete sessionUser.password;
      localStorage.setItem(CURRENT_USER_KEY, JSON.stringify(sessionUser));
      setCurrentUser(sessionUser);
      loadUserData(sessionUser);
      setActiveTab('dashboard');
    } else {
      setAuthError('Kredensial tidak valid!');
    }
  };

  const handleDemoLogin = () => {
    const demoUser = {
      fullName: "Pengguna Demo (Juri)",
      username: "demo_juri",
      email: "demo@jeda.id",
      isDemo: true,
      createdAt: new Date().toISOString(),
      preferences: {
        preferredCategories: ["Spiritualitas", "Regulasi Emosi", "Kebermaknaan Sosial dan Lingkungan"],
        reminderIntervalHours: 3,
        morningJedaTime: "06:00",
        monthlyTarget: 30,
        restrictedApps: ["TikTok", "Instagram"]
      }
    };
    localStorage.setItem(CURRENT_USER_KEY, JSON.stringify(demoUser));
    initUserDataStore(demoUser.username, true);
    setCurrentUser(demoUser);
    loadUserData(demoUser);
    setActiveTab('dashboard');
  };

  const handleRegisterSubmit = (e) => {
    e.preventDefault();
    setAuthError('');
    if (!formData.agreeTerms) return setAuthError('Harap menyetujui syarat dan ketentuan.');
    if (formData.password !== formData.confirmPassword) return setAuthError('Konfirmasi kata sandi tidak cocok.');

    const users = getRegisteredUsers();
    if (users.find(u => u.email === formData.email || u.username === formData.username)) {
      return setAuthError('Email atau Username sudah terdaftar.');
    }

    const newUser = {
      fullName: formData.fullName,
      username: formData.username,
      email: formData.email,
      password: formData.password,
      createdAt: new Date().toISOString(),
      preferences: userPreferences
    };

    users.push(newUser);
    localStorage.setItem(USERS_KEY, JSON.stringify(users));
    initUserDataStore(newUser.username, false);

    const sessionUser = { ...newUser };
    delete sessionUser.password;
    localStorage.setItem(CURRENT_USER_KEY, JSON.stringify(sessionUser));
    setCurrentUser(sessionUser);
    loadUserData(sessionUser);
    setAuthTab('onboarding');
  };

  const handleLogout = () => {
    localStorage.removeItem(CURRENT_USER_KEY);
    setCurrentUser(null);
    setAuthTab('welcome');
    setActiveTab('dashboard');
  };

  const getRandomChallenge = (category = null) => {
    let pool = INITIAL_CHALLENGES;
    if (category && category !== 'Semua') {
      pool = pool.filter(c => c.category === category);
    }
    if (history.length > 0 && pool.length > 1) {
      const lastId = history[0].challengeId;
      pool = pool.filter(c => c.id !== lastId);
    }
    const randomIndex = Math.floor(Math.random() * pool.length);
    setCurrentChallenge(pool[randomIndex] || INITIAL_CHALLENGES[0]);
    setReflectionInput('');
  };

  const handleSaveCheckIn = (emotion) => {
    if (!currentUser) return;
    const newCheckIn = { id: Date.now(), date: new Date().toISOString(), emotion };
    const updated = [newCheckIn, ...checkIns];
    setCheckIns(updated);
    saveUserData(currentUser.username, 'checkins', updated);
  };

  const handleCompleteChallenge = () => {
    if (!currentChallenge || !currentUser) return;
    const record = {
      id: 'hist-' + Date.now(),
      challengeId: currentChallenge.id,
      title: currentChallenge.title,
      category: currentChallenge.category,
      completedAt: new Date().toISOString(),
      durationMinutes: currentChallenge.durationMinutes,
      reflection: currentChallenge.hasReflection ? reflectionInput : null
    };
    const updated = [record, ...history];
    setHistory(updated);
    saveUserData(currentUser.username, 'history', updated);
    setCurrentChallenge(null);
    setReflectionInput('');
    setActiveTab('history');
  };

  const handleSaveAffirmation = () => {
    if (!morningText.trim() || !currentUser) return;
    const newAff = { id: 'aff-' + Date.now(), date: new Date().toISOString().split('T')[0], text: morningText };
    const updated = [newAff, ...affirmations];
    setAffirmations(updated);
    saveUserData(currentUser.username, 'affirmations', updated);
    setMorningText('');
    setActiveTab('history');
  };

  // Calculations
  const totalCompleted = history.length;
  const totalMinutes = history.reduce((acc, item) => acc + (item.durationMinutes || 0), 0);
  const todayDateStr = new Date().toISOString().split('T')[0];
  const todayCount = history.filter(h => h.completedAt.startsWith(todayDateStr)).length;
  const targetPercent = Math.min(Math.round((totalCompleted / userPreferences.monthlyTarget) * 100), 100);

  // ==========================================
  // VIEW: UNAUTHENTICATED (WELCOME / AUTH)
  // ==========================================
  if (!currentUser) {
    return (
      <div className="min-h-screen bg-[#fdfbf7] text-[#2c3b2c] flex flex-col justify-between p-4 md:p-8">
        <header className="max-w-5xl mx-auto w-full flex justify-between items-center py-4">
          <div className="flex items-center gap-2">
            <div className="w-10 h-10 rounded-full bg-[#6b8e6b] flex items-center justify-center text-white font-bold text-xl shadow-sm">J</div>
            <span className="text-2xl font-semibold tracking-wide text-[#354835]">JEDA</span>
          </div>
          <div className="flex items-center gap-3">
            <button onClick={() => { setAuthTab('login'); setAuthError(''); }} className="px-4 py-2 text-sm font-medium text-[#435b43] hover:text-[#2c3b2c] transition">Masuk</button>
            <button onClick={() => { setAuthTab('register'); setAuthError(''); }} className="px-4 py-2 text-sm font-medium bg-[#547254] hover:bg-[#435b43] text-white rounded-xl shadow-sm transition">Daftar Sekarang</button>
          </div>
        </header>

        <main className="max-w-4xl mx-auto w-full my-auto py-8">
          {authTab === 'welcome' && (
            <div className="text-center space-y-6">
              <span className="inline-block px-4 py-1.5 rounded-full bg-[#e3ebe3] text-[#435b43] text-sm font-medium">Prototype Inovasi Kesejahteraan Digital</span>
              <h1 className="text-4xl md:text-5xl font-extrabold text-[#2c3b2c] leading-tight">Berhenti sejenak.<br/>Kembali pada dirimu.</h1>
              <p className="text-lg text-[#435b43] max-w-2xl mx-auto leading-relaxed">JEDA membantu pengguna membangun kebiasaan menggunakan teknologi secara lebih sadar melalui jeda digital, refleksi diri, spiritualitas, dan tindakan positif.</p>
              
              <div className="pt-4 flex flex-col sm:flex-row items-center justify-center gap-4">
                <button onClick={handleDemoLogin} className="w-full sm:w-auto px-8 py-4 bg-[#547254] hover:bg-[#435b43] text-white rounded-2xl font-medium shadow-md transition flex items-center justify-center gap-2">
                  <Sparkles className="w-5 h-5" /> Lihat Demo (Tanpa Daftar)
                </button>
                <button onClick={() => { setAuthTab('register'); setAuthError(''); }} className="w-full sm:w-auto px-8 py-4 bg-white hover:bg-[#f4f7f4] border border-[#c7d7c7] text-[#2c3b2c] rounded-2xl font-medium shadow-sm transition">Buat Akun Baru</button>
              </div>

              <div className="grid grid-cols-1 md:grid-cols-3 gap-4 pt-12 text-left">
                <div className="p-6 bg-white/80 rounded-2xl border border-[#e3ebe3] shadow-sm">
                  <div className="w-10 h-10 rounded-xl bg-[#e3ebe3] flex items-center justify-center text-[#435b43] mb-4"><Compass className="w-5 h-5" /></div>
                  <h3 className="font-semibold text-lg mb-2">30 Challenge Refleksi</h3>
                  <p className="text-sm text-[#547254]">Latihan mindfulness, spiritualitas, dan koneksi sosial secara acak.</p>
                </div>
                <div className="p-6 bg-white/80 rounded-2xl border border-[#e3ebe3] shadow-sm">
                  <div className="w-10 h-10 rounded-xl bg-[#e3ebe3] flex items-center justify-center text-[#435b43] mb-4"><Heart className="w-5 h-5" /></div>
                  <h3 className="font-semibold text-lg mb-2">Check-in Emosi</h3>
                  <p className="text-sm text-[#547254]">Pahami suasana hati secara teratur sebelum kembali ke linimasa.</p>
                </div>
                <div className="p-6 bg-white/80 rounded-2xl border border-[#e3ebe3] shadow-sm">
                  <div className="w-10 h-10 rounded-xl bg-[#e3ebe3] flex items-center justify-center text-[#435b43] mb-4"><Sun className="w-5 h-5" /></div>
                  <h3 className="font-semibold text-lg mb-2">Afirmasi Pagi</h3>
                  <p className="text-sm text-[#547254]">Mulai harimu dengan kesadaran diri dan niat positif.</p>
                </div>
              </div>
            </div>
          )}

          {authTab === 'login' && (
            <div className="max-w-md mx-auto bg-white p-8 rounded-3xl border border-[#e3ebe3] shadow-sm">
              <h2 className="text-2xl font-bold text-[#354835] mb-2">Selamat Datang Kembali</h2>
              <p className="text-sm text-[#547254] mb-6">Masuk untuk melanjutkan perjalanan kesadaran digitalmu.</p>
              {authError && <div className="mb-4 p-3 bg-red-50 text-red-600 text-sm rounded-xl border border-red-100">{authError}</div>}
              
              <form onSubmit={handleLoginSubmit} className="space-y-4">
                <div>
                  <label className="block text-sm font-medium text-[#435b43] mb-1">Email atau Username</label>
                  <input type="text" required className="w-full px-4 py-2.5 rounded-xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b]" placeholder="demo / email" value={formData.username} onChange={(e) => setFormData({...formData, username: e.target.value})} />
                </div>
                <div>
                  <label className="block text-sm font-medium text-[#435b43] mb-1">Kata Sandi</label>
                  <div className="relative">
                    <input type={showPassword ? "text" : "password"} required className="w-full px-4 py-2.5 rounded-xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b] pr-10" placeholder="••••••••" value={formData.password} onChange={(e) => setFormData({...formData, password: e.target.value})} />
                    <button type="button" onClick={() => setShowPassword(!showPassword)} className="absolute right-3 top-3 text-[#547254] hover:text-[#2c3b2c]">{showPassword ? <EyeOff className="w-4 h-4" /> : <Eye className="w-4 h-4" />}</button>
                  </div>
                </div>

                <div className="flex items-center justify-between text-sm">
                  <label className="flex items-center gap-2 text-[#547254] cursor-pointer">
                    <input type="checkbox" className="rounded border-[#c7d7c7] text-[#547254] focus:ring-[#6b8e6b]" /> Ingat saya
                  </label>
                  <button type="button" onClick={() => setResetSimulated(true)} className="text-[#547254] hover:underline">Lupa kata sandi?</button>
                </div>

                {resetSimulated && <div className="p-3 bg-[#f4f7f4] border border-[#c7d7c7] rounded-xl text-xs text-[#354835]"><strong>Simulasi:</strong> Tautan pemulihan email telah disimulasikan.</div>}

                <button type="submit" className="w-full py-3 bg-[#547254] hover:bg-[#435b43] text-white font-medium rounded-xl shadow-sm transition">Masuk</button>
              </form>
              <div className="mt-6 text-center text-sm text-[#547254]">
                Belum punya akun? <button onClick={() => { setAuthTab('register'); setAuthError(''); }} className="text-[#354835] font-semibold hover:underline">Daftar sekarang</button>
              </div>
            </div>
          )}

          {authTab === 'register' && (
            <div className="max-w-md mx-auto bg-white p-8 rounded-3xl border border-[#e3ebe3] shadow-sm">
              <h2 className="text-2xl font-bold text-[#354835] mb-2">Mulai Perjalanan JEDA</h2>
              <p className="text-sm text-[#547254] mb-6">Buat akun pribadi untuk menyimpan riwayat refleksimu.</p>
              {authError && <div className="mb-4 p-3 bg-red-50 text-red-600 text-sm rounded-xl border border-red-100">{authError}</div>}

              <form onSubmit={handleRegisterSubmit} className="space-y-4">
                <div>
                  <label className="block text-sm font-medium text-[#435b43] mb-1">Nama Lengkap</label>
                  <input type="text" required className="w-full px-4 py-2.5 rounded-xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b]" placeholder="Budi Pratama" value={formData.fullName} onChange={(e) => setFormData({...formData, fullName: e.target.value})} />
                </div>
                <div>
                  <label className="block text-sm font-medium text-[#435b43] mb-1">Username</label>
                  <input type="text" required className="w-full px-4 py-2.5 rounded-xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b]" placeholder="budipratama" value={formData.username} onChange={(e) => setFormData({...formData, username: e.target.value})} />
                </div>
                <div>
                  <label className="block text-sm font-medium text-[#435b43] mb-1">Alamat Email</label>
                  <input type="email" required className="w-full px-4 py-2.5 rounded-xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b]" placeholder="budi@example.com" value={formData.email} onChange={(e) => setFormData({...formData, email: e.target.value})} />
                </div>
                <div>
                  <label className="block text-sm font-medium text-[#435b43] mb-1">Kata Sandi</label>
                  <input type="password" required className="w-full px-4 py-2.5 rounded-xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b]" placeholder="Minimal 6 karakter" value={formData.password} onChange={(e) => setFormData({...formData, password: e.target.value})} />
                </div>
                <div>
                  <label className="block text-sm font-medium text-[#435b43] mb-1">Konfirmasi Kata Sandi</label>
                  <input type="password" required className="w-full px-4 py-2.5 rounded-xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b]" placeholder="Ketik ulang kata sandi" value={formData.confirmPassword} onChange={(e) => setFormData({...formData, confirmPassword: e.target.value})} />
                </div>
                <div className="flex items-start gap-2 pt-2">
                  <input type="checkbox" id="terms" required className="mt-1 rounded border-[#c7d7c7] text-[#547254] focus:ring-[#6b8e6b]" checked={formData.agreeTerms} onChange={(e) => setFormData({...formData, agreeTerms: e.target.checked})} />
                  <label htmlFor="terms" className="text-xs text-[#547254]">Saya menyetujui Kebijakan Privasi JEDA. Data disimpan secara lokal.</label>
                </div>
                <button type="submit" className="w-full py-3 bg-[#547254] hover:bg-[#435b43] text-white font-medium rounded-xl shadow-sm transition">Buat Akun</button>
              </form>
              <div className="mt-6 text-center text-sm text-[#547254]">
                Sudah punya akun? <button onClick={() => { setAuthTab('login'); setAuthError(''); }} className="text-[#354835] font-semibold hover:underline">Masuk</button>
              </div>
            </div>
          )}

          {authTab === 'onboarding' && (
            <div className="max-w-xl mx-auto bg-white p-8 rounded-3xl border border-[#e3ebe3] shadow-sm space-y-6 text-center">
              <span className="text-xs font-bold text-[#6b8e6b] uppercase tracking-wider">Langkah Onboarding</span>
              <h2 className="text-2xl font-bold text-[#354835]">Atur Preferensi JEDA-mu</h2>
              <p className="text-sm text-[#547254]">Pilih interval pengingat yang paling nyaman bagimu.</p>
              
              <div className="grid grid-cols-3 gap-3 pt-4">
                {[2, 3, 5].map(hrs => (
                  <button key={hrs} onClick={() => setUserPreferences({...userPreferences, reminderIntervalHours: hrs})} className={`py-3 text-sm rounded-xl border ${userPreferences.reminderIntervalHours === hrs ? 'bg-[#547254] text-white border-[#547254]' : 'bg-white text-[#354835] border-[#c7d7c7]'}`}>
                    Setiap {hrs} Jam
                  </button>
                ))}
              </div>

              <button onClick={() => setActiveTab('dashboard')} className="w-full py-3 bg-[#547254] hover:bg-[#435b43] text-white font-medium rounded-xl shadow-sm transition">Selesaikan & Masuk ke Dashboard</button>
            </div>
          )}
        </main>

        <footer className="max-w-5xl mx-auto w-full text-center text-xs text-[#547254] py-4">Prototype JEDA — Platform Digital Kesejahteraan & Regulasi Emosi</footer>
      </div>
    );
  }

  // ==========================================
  // VIEW: AUTHENTICATED (MAIN APP DASHBOARD)
  // ==========================================
  return (
    <div className="min-h-screen bg-[#fdfbf7] text-[#2c3b2c] flex flex-col md:flex-row">
      {/* Sidebar Nav */}
      <aside className="w-full md:w-64 bg-white border-r border-[#e3ebe3] flex flex-col justify-between p-4 md:p-6 shrink-0">
        <div className="space-y-6">
          <div className="flex items-center gap-3 px-2">
            <div className="w-9 h-9 rounded-xl bg-[#547254] flex items-center justify-center text-white font-bold text-lg shadow-sm">J</div>
            <div>
              <h1 className="text-xl font-bold tracking-wide text-[#354835]">JEDA</h1>
              <p className="text-[10px] text-[#547254]">Ruang Refleksi Digital</p>
            </div>
          </div>

          <nav className="space-y-1">
            <button onClick={() => setActiveTab('dashboard')} className={`w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-medium transition ${activeTab === 'dashboard' ? 'bg-[#e3ebe3] text-[#354835]' : 'text-[#547254] hover:bg-[#f4f7f4]'}`}><Sparkles className="w-4 h-4" /> Beranda</button>
            <button onClick={() => setActiveTab('challenge')} className={`w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-medium transition ${activeTab === 'challenge' ? 'bg-[#e3ebe3] text-[#354835]' : 'text-[#547254] hover:bg-[#f4f7f4]'}`}><Compass className="w-4 h-4" /> Mulai Jeda</button>
            <button onClick={() => setActiveTab('morning')} className={`w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-medium transition ${activeTab === 'morning' ? 'bg-[#e3ebe3] text-[#354835]' : 'text-[#547254] hover:bg-[#f4f7f4]'}`}><Sun className="w-4 h-4" /> Jeda Pagi</button>
            <button onClick={() => setActiveTab('history')} className={`w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-medium transition ${activeTab === 'history' ? 'bg-[#e3ebe3] text-[#354835]' : 'text-[#547254] hover:bg-[#f4f7f4]'}`}><History className="w-4 h-4" /> Perjalananku</button>
            <button onClick={() => setActiveTab('settings')} className={`w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-sm font-medium transition ${activeTab === 'settings' ? 'bg-[#e3ebe3] text-[#354835]' : 'text-[#547254] hover:bg-[#f4f7f4]'}`}><Settings className="w-4 h-4" /> Pengaturan</button>
          </nav>
        </div>

        <div className="pt-6 border-t border-[#e3ebe3] space-y-3">
          <button onClick={() => setActiveTab('profile')} className="w-full flex items-center gap-3 p-2 rounded-xl hover:bg-[#f4f7f4] text-left transition">
            <div className="w-8 h-8 rounded-full bg-[#c7d7c7] text-[#435b43] flex items-center justify-center font-bold text-xs">
              {currentUser.fullName ? currentUser.fullName.charAt(0).toUpperCase() : 'U'}
            </div>
            <div className="flex-1 min-w-0">
              <p className="text-xs font-semibold text-[#354835] truncate">{currentUser.fullName || 'Pengguna'}</p>
              <p className="text-[10px] text-[#547254] truncate">@{currentUser.username}</p>
            </div>
          </button>
          <button onClick={handleLogout} className="w-full flex items-center gap-2 px-3 py-2 text-xs font-medium text-red-600 hover:bg-red-50 rounded-xl transition">
            <LogOut className="w-3.5 h-3.5" /> Keluar
          </button>
        </div>
      </aside>

      {/* Main Content Area */}
      <main className="flex-1 p-4 md:p-8 max-w-5xl overflow-y-auto">
        {/* DASHBOARD */}
        {activeTab === 'dashboard' && (
          <div className="space-y-6">
            <div className="bg-gradient-to-r from-[#547254] to-[#435b43] text-white p-6 md:p-8 rounded-3xl shadow-sm">
              <p className="text-[#e3ebe3] text-sm font-medium mb-1">Halo, selamat datang kembali</p>
              <h2 className="text-2xl md:text-3xl font-bold mb-3">Sudahkah kamu memberi ruang untuk dirimu hari ini?</h2>
              <p className="text-xs md:text-sm text-[#e3ebe3] max-w-xl leading-relaxed">Jeda bukan berarti tertinggal. Jeda adalah keberanian untuk hadir penuh sebelum melanjutkan langkahmu.</p>
            </div>

            <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div className="bg-white p-5 rounded-2xl border border-[#e3ebe3] shadow-sm"><span className="text-xs text-[#547254] font-medium">Jeda Hari Ini</span><p className="text-2xl font-bold text-[#354835] mt-1">{todayCount}</p></div>
              <div className="bg-white p-5 rounded-2xl border border-[#e3ebe3] shadow-sm"><span className="text-xs text-[#547254] font-medium">Total Selesai</span><p className="text-2xl font-bold text-[#354835] mt-1">{totalCompleted}</p></div>
              <div className="bg-white p-5 rounded-2xl border border-[#e3ebe3] shadow-sm"><span className="text-xs text-[#547254] font-medium">Total Durasi</span><p className="text-2xl font-bold text-[#354835] mt-1">{totalMinutes} mnt</p></div>
              <div className="bg-white p-5 rounded-2xl border border-[#e3ebe3] shadow-sm"><span className="text-xs text-[#547254] font-medium">Target Bulanan</span><p className="text-2xl font-bold text-[#354835] mt-1">{targetPercent}%</p></div>
            </div>

            <div className="bg-white p-6 rounded-3xl border border-[#e3ebe3] shadow-sm space-y-4">
              <div>
                <h3 className="text-lg font-semibold text-[#354835]">Bagaimana perasaanmu saat ini?</h3>
                <p className="text-xs text-[#547254]">Pilih emosi yang paling menggambarkan kondisimu sekarang.</p>
              </div>
              <div className="grid grid-cols-3 sm:grid-cols-6 gap-3">
                {[{ label: "Bahagia", icon: "😊" }, { label: "Tenang", icon: "🍃" }, { label: "Biasa saja", icon: "😐" }, { label: "Cemas", icon: "😰" }, { label: "Sedih", icon: "🌧️" }, { label: "Lelah", icon: "🔋" }].map((item) => (
                  <button key={item.label} onClick={() => handleSaveCheckIn(item.label)} className="p-3 bg-[#fdfbf7] hover:bg-[#e3ebe3] border border-[#e3ebe3] rounded-2xl flex flex-col items-center gap-1 transition text-center">
                    <span className="text-xl">{item.icon}</span>
                    <span className="text-xs font-medium text-[#435b43]">{item.label}</span>
                  </button>
                ))}
              </div>
              {checkIns.length > 0 && <div className="pt-2 text-xs text-[#547254] border-t border-[#f4f7f4]">Check-in terakhir: <strong className="text-[#354835]">{checkIns[0].emotion}</strong> ({new Date(checkIns[0].date).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})})</div>}
            </div>

            <div className="bg-[#f4f7f4] p-6 rounded-3xl border border-[#c7d7c7] flex flex-col sm:flex-row items-center justify-between gap-4">
              <div className="space-y-1 text-center sm:text-left">
                <span className="inline-block px-3 py-1 bg-[#c7d7c7] text-[#354835] text-[10px] font-semibold rounded-full uppercase">Tantangan Berikutnya</span>
                <h3 className="text-lg font-bold text-[#354835]">Siap mengambil satu jeda singkat?</h3>
                <p className="text-xs text-[#547254]">Sistem akan memilihkan latihan acak untukmu.</p>
              </div>
              <button onClick={() => { getRandomChallenge(); setActiveTab('challenge'); }} className="px-6 py-3 bg-[#547254] hover:bg-[#435b43] text-white font-medium text-sm rounded-2xl shadow-sm transition shrink-0 flex items-center gap-2">
                <Play className="w-4 h-4" /> Mulai Jeda Sekarang
              </button>
            </div>
          </div>
        )}

        {/* CHALLENGE TAB */}
        {activeTab === 'challenge' && (
          <div className="space-y-6">
            <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
              <div>
                <h2 className="text-2xl font-bold text-[#354835]">Challenge JEDA</h2>
                <p className="text-xs text-[#547254]">Ambil waktu sejenak untuk meregulasi emosi dan pikiranmu.</p>
              </div>
              <div className="flex gap-2 overflow-x-auto pb-2 sm:pb-0">
                {['Semua', 'Spiritualitas', 'Regulasi Emosi', 'Kebermaknaan Sosial dan Lingkungan'].map((cat) => (
                  <button key={cat} onClick={() => { setSelectedCategoryFilter(cat); getRandomChallenge(cat); }} className={`px-3 py-1.5 text-xs font-medium rounded-xl whitespace-nowrap transition ${selectedCategoryFilter === cat ? 'bg-[#547254] text-white' : 'bg-white text-[#435b43] border border-[#c7d7c7]'}`}>
                    {cat}
                  </button>
                ))}
              </div>
            </div>

            {!currentChallenge ? (
              <div className="bg-white p-8 rounded-3xl border border-[#e3ebe3] text-center space-y-4">
                <Compass className="w-12 h-12 text-[#6b8e6b] mx-auto" />
                <h3 className="text-lg font-semibold text-[#354835]">Belum ada challenge yang dipilih</h3>
                <button onClick={() => getRandomChallenge(selectedCategoryFilter)} className="px-6 py-3 bg-[#547254] hover:bg-[#435b43] text-white font-medium text-sm rounded-2xl shadow-sm transition">
                  Ambil Challenge Acak
                </button>
              </div>
            ) : (
              <div className="bg-white p-6 md:p-8 rounded-3xl border border-[#c7d7c7] shadow-sm space-y-6">
                <div className="flex items-center justify-between border-b border-[#e3ebe3] pb-4">
                  <span className="px-3 py-1 bg-[#e3ebe3] text-[#435b43] text-xs font-semibold rounded-full">{currentChallenge.category}</span>
                  <span className="text-xs text-[#547254] flex items-center gap-1"><Clock className="w-3.5 h-3.5" /> Est. {currentChallenge.durationMinutes} Menit</span>
                </div>

                <div className="space-y-3">
                  <h3 className="text-xl font-bold text-[#354835]">{currentChallenge.title}</h3>
                  <p className="text-sm text-[#435b43] leading-relaxed bg-[#fdfbf7] p-4 rounded-2xl border border-[#eee7d8]">"{currentChallenge.instruction}"</p>
                </div>

                {currentChallenge.hasReflection && (
                  <div className="space-y-2">
                    <label className="block text-xs font-semibold text-[#435b43]">Refleksi: {currentChallenge.prompt}</label>
                    <textarea rows={4} className="w-full p-3 text-sm rounded-2xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b]" placeholder="Tuliskan renunganmu di sini..." value={reflectionInput} onChange={(e) => setReflectionInput(e.target.value)} />
                  </div>
                )}

                <div className="flex flex-col sm:flex-row items-center justify-end gap-3 pt-4 border-t border-[#e3ebe3]">
                  <button onClick={() => setCurrentChallenge(null)} className="w-full sm:w-auto px-5 py-2.5 text-xs font-medium text-[#547254] hover:bg-[#f4f7f4] rounded-xl transition">Lewati</button>
                  <button onClick={() => getRandomChallenge(selectedCategoryFilter)} className="w-full sm:w-auto px-5 py-2.5 text-xs font-medium bg-[#e3ebe3] text-[#435b43] hover:bg-[#c7d7c7] rounded-xl transition flex items-center justify-center gap-1"><RotateCcw className="w-3.5 h-3.5" /> Ganti Challenge</button>
                  <button onClick={handleCompleteChallenge} className="w-full sm:w-auto px-6 py-2.5 text-xs font-medium bg-[#547254] hover:bg-[#435b43] text-white rounded-xl shadow-sm transition flex items-center justify-center gap-1"><CheckCircle className="w-3.5 h-3.5" /> Tandai Selesai</button>
                </div>
              </div>
            )}
          </div>
        )}

        {/* MORNING TAB */}
        {activeTab === 'morning' && (
          <div className="space-y-6">
            <div>
              <h2 className="text-2xl font-bold text-[#354835]">Jeda Pagi</h2>
              <p className="text-xs text-[#547254]">Sebelum memulai hari, luangkan waktu untuk dirimu sendiri.</p>
            </div>
            <div className="bg-white p-6 md:p-8 rounded-3xl border border-[#e3ebe3] shadow-sm space-y-6">
              <div className="p-5 bg-amber-50 rounded-2xl border border-amber-100 text-amber-900 space-y-2">
                <span className="text-[10px] font-bold uppercase tracking-wider text-amber-700">Inspirasi Hari Ini</span>
                <p className="text-sm font-medium italic">"Aku berhak menjalani hari ini dengan tenang dan penuh kesadaran tanpa terburu-buru oleh distraksi."</p>
              </div>
              <div className="space-y-3">
                <label className="block text-sm font-semibold text-[#354835]">Tuliskan Afirmasi Pagi Versimu (Target ~30 kata):</label>
                <textarea rows={4} className="w-full p-4 text-sm rounded-2xl border border-[#c7d7c7] focus:outline-none focus:ring-2 focus:ring-[#6b8e6b]" placeholder="Hari ini aku akan fokus menyelesaikan tugas utama sebelum membuka linimasa..." value={morningText} onChange={(e) => setMorningText(e.target.value)} />
                <div className="flex items-center justify-between text-xs text-[#547254]">
                  <span>Jumlah kata: <strong>{morningText.trim() ? morningText.trim().split(/\s+/).length : 0}</strong> / ~30 kata</span>
                </div>
              </div>
              <button onClick={handleSaveAffirmation} disabled={!morningText.trim()} className="w-full py-3 bg-[#547254] hover:bg-[#435b43] disabled:bg-[#c7d7c7] text-white font-medium text-sm rounded-2xl shadow-sm transition">Simpan Afirmasi Pagi</button>
            </div>
          </div>
        )}

        {/* HISTORY TAB */}
        {activeTab === 'history' && (
          <div className="space-y-6">
            <div>
              <h2 className="text-2xl font-bold text-[#354835]">Perjalananku</h2>
              <p className="text-xs text-[#547254]">Catatan jeda, refleksi emosi, dan afirmasi yang telah kamu lalui.</p>
            </div>

            <div className="bg-white p-6 rounded-3xl border border-[#e3ebe3] shadow-sm space-y-2">
              <h3 className="text-sm font-semibold text-[#354835]">Evaluasi Kebiasaan Jeda</h3>
              <p className="text-xs text-[#547254] leading-relaxed">
                {totalCompleted >= userPreferences.monthlyTarget 
                  ? "Kamu telah melakukan lebih banyak jeda daripada target awalmu. Mari lihat apakah pola ini membantu aktivitas digitalmu menjadi lebih seimbang."
                  : `Kamu telah menyelesaikan ${totalCompleted} dari target ${userPreferences.monthlyTarget} jeda bulan ini. Setiap jeda kecil sangat berarti.`}
              </p>
            </div>

            <div className="space-y-4">
              <h3 className="text-base font-bold text-[#354835]">Riwayat Refleksi Challenge</h3>
              {history.length === 0 ? (
                <div className="bg-white p-8 rounded-3xl border border-[#e3ebe3] text-center text-xs text-[#547254]">Belum ada riwayat jeda tersimpan. Mulai challenge pertamamu hari ini!</div>
              ) : (
                history.map((item) => (
                  <div key={item.id} className="bg-white p-5 rounded-2xl border border-[#e3ebe3] shadow-sm space-y-2">
                    <div className="flex items-center justify-between text-xs">
                      <span className="font-semibold text-[#354835]">{item.title}</span>
                      <span className="text-[#547254]">{new Date(item.completedAt).toLocaleDateString()}</span>
                    </div>
                    <span className="inline-block px-2 py-0.5 bg-[#f4f7f4] text-[#547254] text-[10px] rounded-md">{item.category}</span>
                    {item.reflection && <p className="text-xs text-[#435b43] bg-[#fdfbf7] p-3 rounded-xl border border-[#eee7d8] mt-2">"{item.reflection}"</p>}
                  </div>
                ))
              )}
            </div>

            <div className="space-y-4 pt-4 border-t border-[#c7d7c7]">
              <h3 className="text-base font-bold text-[#354835]">Riwayat Afirmasi Pagi</h3>
              {affirmations.length === 0 ? (
                <div className="bg-white p-6 rounded-3xl border border-[#e3ebe3] text-center text-xs text-[#547254]">Belum ada afirmasi pagi tersimpan.</div>
              ) : (
                affirmations.map((aff) => (
                  <div key={aff.id} className="bg-white p-4 rounded-2xl border border-[#e3ebe3] shadow-sm text-xs text-[#435b43]">
                    <span className="block font-semibold text-[#547254] text-[10px] mb-1">{aff.date}</span>
                    "{aff.text}"
                  </div>
                ))
              )}
            </div>
          </div>
        )}

        {/* SETTINGS TAB */}
        {activeTab === 'settings' && (
          <div className="space-y-6">
            <div>
              <h2 className="text-2xl font-bold text-[#354835]">Pengaturan Digital</h2>
              <p className="text-xs text-[#547254]">Sesuaikan preferensi pengingat dan target pribadimu.</p>
            </div>
            <div className="bg-white p-6 rounded-3xl border border-[#e3ebe3] shadow-sm space-y-6">
              <div className="space-y-3">
                <h3 className="text-sm font-semibold text-[#354835]">Interval Pengingat Challenge</h3>
                <div className="grid grid-cols-3 gap-3">
                  {[2, 3, 5].map((hrs) => (
                    <button key={hrs} onClick={() => setUserPreferences({...userPreferences, reminderIntervalHours: hrs})} className={`p-3 text-xs font-medium rounded-2xl border text-center transition ${userPreferences.reminderIntervalHours === hrs ? 'bg-[#547254] text-white border-[#547254]' : 'bg-white text-[#435b43] border-[#c7d7c7]'}`}>
                      Setiap {hrs} Jam
                    </button>
                  ))}
                </div>
              </div>

              <div className="pt-4 border-t border-[#e3ebe3] space-y-2">
                <h3 className="text-sm font-semibold text-[#354835]">Target Jeda Bulanan</h3>
                <input type="number" className="w-full p-3 text-sm rounded-xl border border-[#c7d7c7] focus:ring-2 focus:ring-[#6b8e6b]" value={userPreferences.monthlyTarget} onChange={(e) => setUserPreferences({...userPreferences, monthlyTarget: parseInt(e.target.value) || 30})} />
              </div>

              <div className="pt-6 border-t border-[#e3ebe3] space-y-2">
                <h3 className="text-sm font-semibold text-red-600">Hapus Data Akun Ini</h3>
                <button onClick={() => { if (confirm("Hapus seluruh data riwayat lokal akun ini?")) { clearUserData(currentUser.username); loadUserData(currentUser); } }} className="px-4 py-2 bg-red-50 text-red-600 hover:bg-red-100 border border-red-200 text-xs font-medium rounded-xl transition">Hapus Data</button>
              </div>
            </div>
          </div>
        )}

        {/* PROFILE TAB */}
        {activeTab === 'profile' && (
          <div className="space-y-6">
            <div>
              <h2 className="text-2xl font-bold text-[#354835]">Profil Pengguna</h2>
              <p className="text-xs text-[#547254]">Informasi akun dan status sesi JEDA-mu.</p>
            </div>
            <div className="bg-white p-6 md:p-8 rounded-3xl border border-[#e3ebe3] shadow-sm space-y-6">
              <div className="flex items-center gap-4">
                <div className="w-16 h-16 rounded-2xl bg-[#c7d7c7] text-[#435b43] flex items-center justify-center font-bold text-2xl">
                  {currentUser.fullName ? currentUser.fullName.charAt(0).toUpperCase() : 'U'}
                </div>
                <div>
                  <h3 className="text-lg font-bold text-[#354835]">{currentUser.fullName}</h3>
                  <p className="text-xs text-[#547254]">@{currentUser.username} • {currentUser.email}</p>
                </div>
              </div>
            </div>
          </div>
        )}
      </main>
    </div>
  );
}
