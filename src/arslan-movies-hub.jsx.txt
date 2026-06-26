import { useState, useRef } from "react";

// ─── TRANSLATIONS ─────────────────────────────────────────────────────────────
const T = {
  en: {
    name: "English", flag: "🇬🇧",
    loginTab: "Login", signupTab: "Sign Up",
    email: "Email Address", password: "Password", confirmPass: "Confirm Password",
    fullName: "Full Name", loginBtn: "Login", signupBtn: "Create Account",
    googleBtn: "Continue with Google", orDivider: "OR",
    noAccount: "Don't have an account?", hasAccount: "Already have an account?",
    signupLink: "Sign Up", loginLink: "Login",
    welcomeBack: "Welcome Back!", joinUs: "Join Arslan Movies Hub",
    tagline: "Stream · Upload · Share",
    heroSub: "Upload movies, watch & share with friends!",
    search: "🔍 Search movies...", share: "🔗 Share",
    upload: "+ Upload", myMovies: "My Movies", logout: "Logout",
    totalViews: "total views", movies: "movies",
    noMovies: "No movies found", uploadFirst: "+ Upload First Movie",
    uploadTitle: "Upload New Movie", movieTitle: "Movie Title *",
    movieTitlePlaceholder: "Movie name...", genre: "Genre", year: "Year",
    description: "Description", descPlaceholder: "Write about the movie...",
    selectVideo: "Select Video File", videoSupport: "MP4, MKV, AVI supported",
    thumbnail: "Thumbnail (optional)", uploading: "⏳ Uploading...", uploadBtn: "🚀 Upload",
    backBtn: "Go Back", shareBtn: "🔗 Share Link",
    uploadForLogin: "⚡ Login with Google to upload movies",
    footerText: "Arslan Movies Hub • Share with friends 🔗",
    nameRequired: "Please enter your name!", emailRequired: "Please enter email!",
    passRequired: "Please enter password!", passMatch: "Passwords do not match!",
    loginSuccess: "✅ Welcome back!", signupSuccess: "✅ Account created! Welcome!",
    googleSuccess: "✅ Logged in with Google!",
    titleVideoRequired: "Title and video file required!",
    uploadedSuccess: "🎬 Movie uploaded! Share the link!",
    linkCopied: "🔗 Link copied! Share with friends",
    langLabel: "Language",
  },
  ur: {
    name: "اردو", flag: "🇵🇰",
    loginTab: "لاگ ان", signupTab: "سائن اپ",
    email: "ای میل", password: "پاس ورڈ", confirmPass: "پاس ورڈ دوبارہ",
    fullName: "پورا نام", loginBtn: "لاگ ان کریں", signupBtn: "اکاؤنٹ بنائیں",
    googleBtn: "گوگل سے جاری رکھیں", orDivider: "یا",
    noAccount: "اکاؤنٹ نہیں ہے؟", hasAccount: "پہلے سے اکاؤنٹ ہے؟",
    signupLink: "سائن اپ", loginLink: "لاگ ان",
    welcomeBack: "خوش آمدید!", joinUs: "ارسلان موویز ہب میں شامل ہوں",
    tagline: "دیکھیں · اپلوڈ کریں · شیئر کریں",
    heroSub: "مووی اپلوڈ کریں، دیکھیں اور دوستوں سے شیئر کریں!",
    search: "🔍 مووی تلاش کریں...", share: "🔗 شیئر",
    upload: "+ اپلوڈ", myMovies: "میری موویز", logout: "لاگ آؤٹ",
    totalViews: "کل ویوز", movies: "موویز",
    noMovies: "کوئی مووی نہیں ملی", uploadFirst: "+ پہلی مووی اپلوڈ کریں",
    uploadTitle: "نئی مووی اپلوڈ کریں", movieTitle: "مووی کا عنوان *",
    movieTitlePlaceholder: "مووی کا نام...", genre: "قسم", year: "سال",
    description: "تفصیل", descPlaceholder: "مووی کے بارے میں لکھیں...",
    selectVideo: "ویڈیو فائل منتخب کریں", videoSupport: "MP4, MKV, AVI قابل قبول",
    thumbnail: "تھمب نیل (اختیاری)", uploading: "⏳ اپلوڈ ہو رہا ہے...", uploadBtn: "🚀 اپلوڈ کریں",
    backBtn: "واپس جائیں", shareBtn: "🔗 لنک شیئر کریں",
    uploadForLogin: "⚡ مووی اپلوڈ کرنے کے لیے گوگل سے لاگ ان کریں",
    footerText: "ارسلان موویز ہب • دوستوں سے شیئر کریں 🔗",
    nameRequired: "نام درج کریں!", emailRequired: "ای میل درج کریں!",
    passRequired: "پاس ورڈ درج کریں!", passMatch: "پاس ورڈ مماثل نہیں!",
    loginSuccess: "✅ خوش آمدید!", signupSuccess: "✅ اکاؤنٹ بن گیا! خوش آمدید!",
    googleSuccess: "✅ گوگل سے لاگ ان ہو گئے!",
    titleVideoRequired: "عنوان اور ویڈیو فائل ضروری ہے!",
    uploadedSuccess: "🎬 مووی اپلوڈ ہو گئی! لنک شیئر کریں!",
    linkCopied: "🔗 لنک کاپی ہو گیا! دوستوں کو بھیجیں",
    langLabel: "زبان",
  },
  hi: {
    name: "हिंदी", flag: "🇮🇳",
    loginTab: "लॉगिन", signupTab: "साइन अप",
    email: "ईमेल पता", password: "पासवर्ड", confirmPass: "पासवर्ड दोबारा",
    fullName: "पूरा नाम", loginBtn: "लॉगिन करें", signupBtn: "अकाउंट बनाएं",
    googleBtn: "Google से जारी रखें", orDivider: "या",
    noAccount: "अकाउंट नहीं है?", hasAccount: "पहले से अकाउंट है?",
    signupLink: "साइन अप", loginLink: "लॉगिन",
    welcomeBack: "वापसी पर स्वागत!", joinUs: "Arslan Movies Hub में शामिल हों",
    tagline: "देखें · अपलोड करें · शेयर करें",
    heroSub: "मूवी अपलोड करें, देखें और दोस्तों के साथ शेयर करें!",
    search: "🔍 मूवी खोजें...", share: "🔗 शेयर",
    upload: "+ अपलोड", myMovies: "मेरी मूवीज़", logout: "लॉगआउट",
    totalViews: "कुल व्यूज़", movies: "मूवीज़",
    noMovies: "कोई मूवी नहीं मिली", uploadFirst: "+ पहली मूवी अपलोड करें",
    uploadTitle: "नई मूवी अपलोड करें", movieTitle: "मूवी का शीर्षक *",
    movieTitlePlaceholder: "मूवी का नाम...", genre: "शैली", year: "साल",
    description: "विवरण", descPlaceholder: "मूवी के बारे में लिखें...",
    selectVideo: "वीडियो फ़ाइल चुनें", videoSupport: "MP4, MKV, AVI समर्थित",
    thumbnail: "थंबनेल (वैकल्पिक)", uploading: "⏳ अपलोड हो रहा है...", uploadBtn: "🚀 अपलोड करें",
    backBtn: "वापस जाएं", shareBtn: "🔗 लिंक शेयर करें",
    uploadForLogin: "⚡ मूवी अपलोड करने के लिए Google से लॉगिन करें",
    footerText: "Arslan Movies Hub • दोस्तों के साथ शेयर करें 🔗",
    nameRequired: "नाम दर्ज करें!", emailRequired: "ईमेल दर्ज करें!",
    passRequired: "पासवर्ड दर्ज करें!", passMatch: "पासवर्ड मेल नहीं खाते!",
    loginSuccess: "✅ स्वागत है!", signupSuccess: "✅ अकाउंट बन गया! स्वागत है!",
    googleSuccess: "✅ Google से लॉगिन हो गए!",
    titleVideoRequired: "शीर्षक और वीडियो फ़ाइल ज़रूरी है!",
    uploadedSuccess: "🎬 मूवी अपलोड हो गई! लिंक शेयर करें!",
    linkCopied: "🔗 लिंक कॉपी हो गया! दोस्तों को भेजें",
    langLabel: "भाषा",
  },
};

// ─── Sample Movies ────────────────────────────────────────────────────────────
const SAMPLE_MOVIES = [
  { id: 1, title: "Interstellar", genre: "Sci-Fi", year: 2014, rating: 8.6, thumbnail: "https://picsum.photos/seed/inter/400/220", url: "https://www.w3schools.com/html/mov_bbb.mp4", uploadedBy: "Admin", views: 1240, description: "A team of explorers travel through a wormhole in space." },
  { id: 2, title: "The Dark Knight", genre: "Action", year: 2008, rating: 9.0, thumbnail: "https://picsum.photos/seed/dark/400/220", url: "https://www.w3schools.com/html/mov_bbb.mp4", uploadedBy: "Admin", views: 3890, description: "Batman faces the Joker in a battle for Gotham City." },
  { id: 3, title: "Inception", genre: "Thriller", year: 2010, rating: 8.8, thumbnail: "https://picsum.photos/seed/incep/400/220", url: "https://www.w3schools.com/html/mov_bbb.mp4", uploadedBy: "Admin", views: 2100, description: "A thief who steals corporate secrets through dream-sharing." },
  { id: 4, title: "Avengers: Endgame", genre: "Action", year: 2019, rating: 8.4, thumbnail: "https://picsum.photos/seed/aveng/400/220", url: "https://www.w3schools.com/html/mov_bbb.mp4", uploadedBy: "Admin", views: 5600, description: "The Avengers assemble one last time to defeat Thanos." },
];

const GENRES = ["All", "Action", "Sci-Fi", "Thriller", "Drama", "Comedy", "Horror"];

// ─── MAIN APP ─────────────────────────────────────────────────────────────────
export default function ArslanMoviesHub() {
  const [lang, setLang] = useState("en");
  const t = T[lang];
  const isRtl = lang === "ur";

  // Auth state
  const [authScreen, setAuthScreen] = useState(true); // true = show login/signup
  const [authTab, setAuthTab] = useState("login");
  const [user, setUser] = useState(null);

  // Login form
  const [loginForm, setLoginForm] = useState({ email: "", password: "" });
  const [signupForm, setSignupForm] = useState({ name: "", email: "", password: "", confirm: "" });

  // App state
  const [movies, setMovies] = useState(SAMPLE_MOVIES);
  const [search, setSearch] = useState("");
  const [genre, setGenre] = useState("All");
  const [playing, setPlaying] = useState(null);
  const [showUpload, setShowUpload] = useState(false);
  const [showProfile, setShowProfile] = useState(false);
  const [showLangMenu, setShowLangMenu] = useState(false);
  const [uploadForm, setUploadForm] = useState({ title: "", genre: "Action", year: "", description: "", file: null, thumb: null });
  const [uploading, setUploading] = useState(false);
  const [toast, setToast] = useState(null);
  const [page, setPage] = useState("home");
  const fileRef = useRef();
  const thumbRef = useRef();

  const showToast = (msg, type = "success") => {
    setToast({ msg, type });
    setTimeout(() => setToast(null), 3200);
  };

  // ── AUTH ──
  const doLogin = () => {
    if (!loginForm.email) return showToast(t.emailRequired, "error");
    if (!loginForm.password) return showToast(t.passRequired, "error");
    const u = { name: loginForm.email.split("@")[0], email: loginForm.email, photo: `https://ui-avatars.com/api/?name=${loginForm.email.split("@")[0]}&background=e50914&color=fff` };
    setUser(u); setAuthScreen(false); showToast(t.loginSuccess);
  };

  const doSignup = () => {
    if (!signupForm.name) return showToast(t.nameRequired, "error");
    if (!signupForm.email) return showToast(t.emailRequired, "error");
    if (!signupForm.password) return showToast(t.passRequired, "error");
    if (signupForm.password !== signupForm.confirm) return showToast(t.passMatch, "error");
    const u = { name: signupForm.name, email: signupForm.email, photo: `https://ui-avatars.com/api/?name=${signupForm.name}&background=e50914&color=fff` };
    setUser(u); setAuthScreen(false); showToast(t.signupSuccess);
  };

  const doGoogle = () => {
    const u = { name: "Arslan Khan", email: "arslan@gmail.com", photo: "https://ui-avatars.com/api/?name=Arslan+Khan&background=e50914&color=fff" };
    setUser(u); setAuthScreen(false); showToast(t.googleSuccess);
  };

  const doLogout = () => { setUser(null); setAuthScreen(true); setShowProfile(false); setPage("home"); };

  // ── UPLOAD ──
  const handleUpload = () => {
    if (!uploadForm.title || !uploadForm.file) return showToast(t.titleVideoRequired, "error");
    setUploading(true);
    setTimeout(() => {
      setMovies(prev => [{
        id: Date.now(), title: uploadForm.title, genre: uploadForm.genre,
        year: parseInt(uploadForm.year) || new Date().getFullYear(),
        rating: (Math.random() * 2 + 7).toFixed(1),
        thumbnail: uploadForm.thumb ? URL.createObjectURL(uploadForm.thumb) : `https://picsum.photos/seed/${Date.now()}/400/220`,
        url: URL.createObjectURL(uploadForm.file),
        uploadedBy: user?.name || "Guest", views: 0, description: uploadForm.description || "No description.",
      }, ...prev]);
      setUploadForm({ title: "", genre: "Action", year: "", description: "", file: null, thumb: null });
      setShowUpload(false); setUploading(false);
      showToast(t.uploadedSuccess);
    }, 1800);
  };

  const copyLink = () => { navigator.clipboard.writeText(window.location.href); showToast(t.linkCopied); };

  const filtered = movies.filter(m => {
    const matchSearch = m.title.toLowerCase().includes(search.toLowerCase());
    const matchGenre = genre === "All" || m.genre === genre;
    const matchPage = page === "myuploads" ? m.uploadedBy === user?.name : true;
    return matchSearch && matchGenre && matchPage;
  });

  // ── AUTH SCREEN ──
  if (authScreen) return (
    <div dir={isRtl ? "rtl" : "ltr"} style={{ minHeight: "100vh", background: "#07070f", display: "flex", alignItems: "center", justifyContent: "center", fontFamily: "'Segoe UI',system-ui,sans-serif", padding: "1rem", position: "relative", overflow: "hidden" }}>
      {/* Background glow */}
      <div style={{ position: "absolute", inset: 0, background: "radial-gradient(ellipse at 30% 40%, rgba(229,9,20,0.12) 0%, transparent 60%), radial-gradient(ellipse at 70% 70%, rgba(100,0,200,0.08) 0%, transparent 60%)", pointerEvents: "none" }} />

      {/* Toast */}
      {toast && <div style={{ position: "fixed", bottom: 24, right: 24, zIndex: 999, background: toast.type === "error" ? "#c0392b" : "#1a6b1a", color: "#fff", borderRadius: 10, padding: "12px 20px", fontWeight: 600, fontSize: "0.9rem", boxShadow: "0 4px 20px rgba(0,0,0,0.5)", animation: "fadeIn 0.3s" }}>{toast.msg}</div>}

      {/* Lang selector top right */}
      <div style={{ position: "absolute", top: 18, right: 18, zIndex: 10 }}>
        <div style={{ position: "relative" }}>
          <button onClick={() => setShowLangMenu(!showLangMenu)} style={{ background: "rgba(255,255,255,0.07)", border: "1px solid rgba(255,255,255,0.15)", borderRadius: 8, padding: "7px 14px", color: "#fff", cursor: "pointer", fontSize: "0.85rem", display: "flex", alignItems: "center", gap: 6 }}>
            {T[lang].flag} {T[lang].name} ▾
          </button>
          {showLangMenu && (
            <div style={{ position: "absolute", top: "110%", right: 0, background: "#1a1a2e", border: "1px solid rgba(255,255,255,0.12)", borderRadius: 10, overflow: "hidden", minWidth: 140, boxShadow: "0 8px 24px rgba(0,0,0,0.5)" }}>
              {Object.entries(T).map(([code, val]) => (
                <div key={code} onClick={() => { setLang(code); setShowLangMenu(false); }} style={{ padding: "10px 16px", cursor: "pointer", color: lang === code ? "#e50914" : "#ddd", fontWeight: lang === code ? 700 : 400, background: lang === code ? "rgba(229,9,20,0.1)" : "transparent", fontSize: "0.9rem", display: "flex", alignItems: "center", gap: 8 }}>
                  {val.flag} {val.name}
                </div>
              ))}
            </div>
          )}
        </div>
      </div>

      {/* Auth Card */}
      <div style={{ background: "#0f0f1e", borderRadius: 20, border: "1px solid rgba(255,255,255,0.08)", width: "100%", maxWidth: 420, boxShadow: "0 24px 64px rgba(0,0,0,0.6)", overflow: "hidden", position: "relative", zIndex: 2 }}>
        {/* Logo Header */}
        <div style={{ background: "linear-gradient(135deg,#1a0000,#0f0f1e)", padding: "2rem 2rem 1.5rem", textAlign: "center", borderBottom: "1px solid rgba(229,9,20,0.15)" }}>
          <div style={{ display: "inline-flex", alignItems: "center", justifyContent: "center", width: 56, height: 56, background: "linear-gradient(135deg,#e50914,#ff6b35)", borderRadius: 14, fontSize: "1.6rem", boxShadow: "0 0 24px rgba(229,9,20,0.5)", marginBottom: 12 }}>🎬</div>
          <div style={{ fontSize: "1.5rem", fontWeight: 900, color: "#fff", fontFamily: "'Georgia',serif", letterSpacing: 0.5 }}>
            <span style={{ color: "#e50914" }}>Arslan</span> Movies Hub
          </div>
          <div style={{ fontSize: "0.6rem", letterSpacing: "3px", color: "#e50914", textTransform: "uppercase", marginTop: 4, fontWeight: 600 }}>{t.tagline}</div>
        </div>

        {/* Tabs */}
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", borderBottom: "1px solid rgba(255,255,255,0.07)" }}>
          {["login", "signup"].map(tab => (
            <button key={tab} onClick={() => setAuthTab(tab)} style={{ background: authTab === tab ? "rgba(229,9,20,0.12)" : "transparent", color: authTab === tab ? "#e50914" : "#888", border: "none", borderBottom: authTab === tab ? "2px solid #e50914" : "2px solid transparent", padding: "14px", fontWeight: 700, fontSize: "0.95rem", cursor: "pointer", transition: "all 0.2s" }}>
              {tab === "login" ? t.loginTab : t.signupTab}
            </button>
          ))}
        </div>

        {/* Form */}
        <div style={{ padding: "1.5rem 2rem 2rem" }}>
          {authTab === "login" ? (
            <>
              <p style={{ textAlign: "center", color: "#aaa", fontSize: "0.9rem", margin: "0 0 1.2rem" }}>{t.welcomeBack}</p>
              <AuthInput label={t.email} placeholder="you@gmail.com" type="email" value={loginForm.email} onChange={v => setLoginForm(p => ({ ...p, email: v }))} />
              <AuthInput label={t.password} placeholder="••••••••" type="password" value={loginForm.password} onChange={v => setLoginForm(p => ({ ...p, password: v }))} />
              <button onClick={doLogin} style={btnStyle}>{t.loginBtn}</button>
              <Divider label={t.orDivider} />
              <GoogleBtn label={t.googleBtn} onClick={doGoogle} />
              <p style={{ textAlign: "center", color: "#666", fontSize: "0.83rem", marginTop: "1.2rem" }}>
                {t.noAccount} <span onClick={() => setAuthTab("signup")} style={{ color: "#e50914", cursor: "pointer", fontWeight: 700 }}>{t.signupLink}</span>
              </p>
            </>
          ) : (
            <>
              <p style={{ textAlign: "center", color: "#aaa", fontSize: "0.9rem", margin: "0 0 1.2rem" }}>{t.joinUs}</p>
              <AuthInput label={t.fullName} placeholder="Arslan Khan" value={signupForm.name} onChange={v => setSignupForm(p => ({ ...p, name: v }))} />
              <AuthInput label={t.email} placeholder="you@gmail.com" type="email" value={signupForm.email} onChange={v => setSignupForm(p => ({ ...p, email: v }))} />
              <AuthInput label={t.password} placeholder="••••••••" type="password" value={signupForm.password} onChange={v => setSignupForm(p => ({ ...p, password: v }))} />
              <AuthInput label={t.confirmPass} placeholder="••••••••" type="password" value={signupForm.confirm} onChange={v => setSignupForm(p => ({ ...p, confirm: v }))} />
              <button onClick={doSignup} style={btnStyle}>{t.signupBtn}</button>
              <Divider label={t.orDivider} />
              <GoogleBtn label={t.googleBtn} onClick={doGoogle} />
              <p style={{ textAlign: "center", color: "#666", fontSize: "0.83rem", marginTop: "1.2rem" }}>
                {t.hasAccount} <span onClick={() => setAuthTab("login")} style={{ color: "#e50914", cursor: "pointer", fontWeight: 700 }}>{t.loginLink}</span>
              </p>
            </>
          )}
        </div>
      </div>
      <style>{`@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}*{box-sizing:border-box}`}</style>
    </div>
  );

  // ── MAIN HOME ──
  return (
    <div dir={isRtl ? "rtl" : "ltr"} style={{ minHeight: "100vh", background: "#0a0a0f", fontFamily: "'Segoe UI',system-ui,sans-serif", color: "#f0f0f0" }}>

      {/* Toast */}
      {toast && <div style={{ position: "fixed", bottom: 24, right: 24, zIndex: 999, background: toast.type === "error" ? "#c0392b" : "#1a6b1a", color: "#fff", borderRadius: 10, padding: "12px 20px", fontWeight: 600, fontSize: "0.9rem", boxShadow: "0 4px 20px rgba(0,0,0,0.4)", maxWidth: 320, animation: "fadeIn 0.3s" }}>{toast.msg}</div>}

      {/* ── Navbar ── */}
      <nav style={{ background: "linear-gradient(180deg,#000 0%,rgba(0,0,0,0.9) 100%)", padding: "0 1.5rem", display: "flex", alignItems: "center", justifyContent: "space-between", height: 64, position: "sticky", top: 0, zIndex: 100, borderBottom: "1px solid rgba(229,9,20,0.3)", backdropFilter: "blur(12px)", gap: 8 }}>
        {/* Logo */}
        <div style={{ display: "flex", alignItems: "center", gap: 10, cursor: "pointer", flexShrink: 0 }} onClick={() => { setPage("home"); setSearch(""); setGenre("All"); }}>
          <div style={{ width: 38, height: 38, background: "linear-gradient(135deg,#e50914,#ff6b35)", borderRadius: 10, display: "flex", alignItems: "center", justifyContent: "center", fontSize: "1.1rem", boxShadow: "0 0 14px rgba(229,9,20,0.5)", flexShrink: 0 }}>🎬</div>
          <div style={{ display: "flex", flexDirection: "column", lineHeight: 1 }}>
            <span style={{ fontSize: "1.15rem", fontWeight: 900, color: "#fff", fontFamily: "'Georgia',serif" }}><span style={{ color: "#e50914" }}>Arslan</span> Movies Hub</span>
            <span style={{ fontSize: "0.55rem", fontWeight: 600, letterSpacing: "3px", color: "#e50914", textTransform: "uppercase", marginTop: 2 }}>◆ {t.tagline} ◆</span>
          </div>
        </div>

        {/* Nav Right */}
        <div style={{ display: "flex", alignItems: "center", gap: 8, flexWrap: "nowrap" }}>
          {/* Language */}
          <div style={{ position: "relative" }}>
            <button onClick={() => setShowLangMenu(!showLangMenu)} style={{ background: "rgba(255,255,255,0.07)", border: "1px solid rgba(255,255,255,0.15)", borderRadius: 7, padding: "6px 10px", color: "#fff", cursor: "pointer", fontSize: "0.8rem", display: "flex", alignItems: "center", gap: 4 }}>
              {T[lang].flag} ▾
            </button>
            {showLangMenu && (
              <div style={{ position: "absolute", top: "110%", right: 0, background: "#1a1a2e", border: "1px solid rgba(255,255,255,0.12)", borderRadius: 10, overflow: "hidden", minWidth: 140, boxShadow: "0 8px 24px rgba(0,0,0,0.6)", zIndex: 200 }}>
                {Object.entries(T).map(([code, val]) => (
                  <div key={code} onClick={() => { setLang(code); setShowLangMenu(false); }} style={{ padding: "10px 16px", cursor: "pointer", color: lang === code ? "#e50914" : "#ddd", fontWeight: lang === code ? 700 : 400, background: lang === code ? "rgba(229,9,20,0.1)" : "transparent", fontSize: "0.88rem", display: "flex", alignItems: "center", gap: 8 }}>
                    {val.flag} {val.name}
                  </div>
                ))}
              </div>
            )}
          </div>

          <button style={{ background: "transparent", color: "#f0f0f0", border: "1px solid rgba(255,255,255,0.2)", borderRadius: 6, padding: "7px 12px", fontWeight: 600, fontSize: "0.82rem", cursor: "pointer" }} onClick={copyLink}>🔗 {t.share}</button>
          <button style={{ background: "#e50914", color: "#fff", border: "none", borderRadius: 6, padding: "7px 12px", fontWeight: 700, fontSize: "0.82rem", cursor: "pointer" }} onClick={() => setShowUpload(true)}>{t.upload}</button>
          <img src={user?.photo} alt={user?.name} style={{ width: 34, height: 34, borderRadius: "50%", border: "2px solid #e50914", cursor: "pointer" }} onClick={() => setShowProfile(!showProfile)} />
        </div>
      </nav>

      {/* Profile Dropdown */}
      {showProfile && (
        <div style={{ position: "fixed", top: 70, right: 18, zIndex: 300, background: "#1e1e2e", borderRadius: 12, border: "1px solid rgba(255,255,255,0.12)", padding: "1rem", minWidth: 210, boxShadow: "0 8px 32px rgba(0,0,0,0.5)" }}>
          <div style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 12 }}>
            <img src={user?.photo} alt="" style={{ width: 42, height: 42, borderRadius: "50%", border: "2px solid #e50914" }} />
            <div><div style={{ fontWeight: 700, fontSize: "0.95rem" }}>{user?.name}</div><div style={{ fontSize: "0.75rem", color: "#888" }}>{user?.email}</div></div>
          </div>
          <hr style={{ border: "none", borderTop: "1px solid rgba(255,255,255,0.08)", margin: "8px 0" }} />
          <button style={{ background: "rgba(255,255,255,0.07)", color: "#fff", border: "1px solid rgba(255,255,255,0.15)", borderRadius: 6, padding: "8px 12px", width: "100%", cursor: "pointer", marginBottom: 8, fontWeight: 600, fontSize: "0.88rem" }} onClick={() => { setPage("myuploads"); setShowProfile(false); }}>📂 {t.myMovies}</button>
          <button style={{ background: "#333", color: "#fff", border: "none", borderRadius: 6, padding: "8px 12px", width: "100%", cursor: "pointer", fontWeight: 600, fontSize: "0.88rem" }} onClick={doLogout}>🚪 {t.logout}</button>
        </div>
      )}

      {/* Hero */}
      <div style={{ background: "linear-gradient(135deg,#1a0000 0%,#0a0a0f 60%,#00001a 100%)", padding: "3.5rem 2rem 2.5rem", textAlign: "center", borderBottom: "1px solid rgba(229,9,20,0.15)" }}>
        <h1 style={{ fontSize: "clamp(1.8rem,5vw,3.2rem)", fontWeight: 900, margin: 0, lineHeight: 1.1 }}>
          <span style={{ color: "#e50914" }}>Arslan</span> Movies Hub 🍿
        </h1>
        <p style={{ color: "#aaa", marginTop: "0.7rem", fontSize: "1rem" }}>{t.heroSub}</p>
        <div style={{ marginTop: "1.4rem", display: "flex", justifyContent: "center", gap: 8, flexWrap: "wrap" }}>
          <input style={{ background: "rgba(255,255,255,0.08)", border: "1px solid rgba(255,255,255,0.2)", borderRadius: 8, padding: "10px 16px", color: "#fff", fontSize: "1rem", width: "min(380px,80vw)", outline: "none" }} placeholder={t.search} value={search} onChange={e => setSearch(e.target.value)} />
          <button style={{ background: "#e50914", color: "#fff", border: "none", borderRadius: 8, padding: "10px 18px", fontWeight: 700, cursor: "pointer" }} onClick={copyLink}>{t.share}</button>
        </div>
      </div>

      {/* Genre Bar */}
      <div style={{ display: "flex", gap: 8, padding: "1rem 1.5rem", overflowX: "auto", borderBottom: "1px solid rgba(255,255,255,0.07)" }}>
        {GENRES.map(g => (
          <button key={g} onClick={() => setGenre(g)} style={{ background: genre === g ? "#e50914" : "rgba(255,255,255,0.07)", color: "#fff", border: genre === g ? "none" : "1px solid rgba(255,255,255,0.15)", borderRadius: 20, padding: "6px 16px", fontWeight: 600, fontSize: "0.83rem", cursor: "pointer", whiteSpace: "nowrap" }}>{g}</button>
        ))}
      </div>

      {/* Stats */}
      <div style={{ display: "flex", gap: "1.5rem", padding: "0.6rem 1.5rem", background: "rgba(255,255,255,0.02)", fontSize: "0.82rem", color: "#777" }}>
        <span>🎬 {filtered.length} {t.movies}</span>
        <span>👀 {movies.reduce((a, m) => a + m.views, 0).toLocaleString()} {t.totalViews}</span>
        <span>👤 {user?.name}</span>
      </div>

      {/* Grid */}
      {filtered.length === 0 ? (
        <div style={{ textAlign: "center", padding: "4rem 2rem", color: "#555" }}>
          <div style={{ fontSize: "3rem" }}>🎞️</div>
          <p>{t.noMovies}</p>
          <button style={{ background: "#e50914", color: "#fff", border: "none", borderRadius: 6, padding: "10px 20px", fontWeight: 700, cursor: "pointer" }} onClick={() => setShowUpload(true)}>{t.uploadFirst}</button>
        </div>
      ) : (
        <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill,minmax(250px,1fr))", gap: "1.4rem", padding: "1.5rem" }}>
          {filtered.map(movie => (
            <div key={movie.id} style={{ background: "#14141f", borderRadius: 12, overflow: "hidden", border: "1px solid rgba(255,255,255,0.07)", cursor: "pointer", transition: "transform 0.2s,box-shadow 0.2s" }}
              onClick={() => { setPlaying(movie); setMovies(prev => prev.map(m => m.id === movie.id ? { ...m, views: m.views + 1 } : m)); }}
              onMouseEnter={e => { e.currentTarget.style.transform = "translateY(-4px)"; e.currentTarget.style.boxShadow = "0 12px 32px rgba(229,9,20,0.18)"; }}
              onMouseLeave={e => { e.currentTarget.style.transform = ""; e.currentTarget.style.boxShadow = ""; }}>
              <div style={{ position: "relative" }}>
                <img src={movie.thumbnail} alt={movie.title} style={{ width: "100%", height: 155, objectFit: "cover", display: "block" }} />
                <div style={{ position: "absolute", top: 8, right: 8, background: "rgba(0,0,0,0.7)", borderRadius: 6, padding: "2px 8px", fontSize: "0.75rem", color: "#f5c518" }}>⭐ {movie.rating}</div>
              </div>
              <div style={{ padding: "0.8rem 1rem 1rem" }}>
                <div style={{ fontWeight: 700, fontSize: "0.97rem" }}>{movie.title}</div>
                <div style={{ marginTop: 6 }}>
                  <span style={{ display: "inline-block", background: "rgba(229,9,20,0.18)", color: "#e50914", borderRadius: 4, padding: "2px 8px", fontSize: "0.73rem", fontWeight: 700, marginRight: 6 }}>{movie.genre}</span>
                  <span style={{ color: "#888", fontSize: "0.78rem" }}>{movie.year}</span>
                </div>
                <div style={{ color: "#777", fontSize: "0.78rem", marginTop: 6, display: "flex", gap: 10 }}>
                  <span>👁 {movie.views}</span><span>📤 {movie.uploadedBy}</span>
                </div>
              </div>
            </div>
          ))}
        </div>
      )}

      {/* Video Modal */}
      {playing && (
        <div style={{ position: "fixed", inset: 0, background: "rgba(0,0,0,0.9)", zIndex: 200, display: "flex", alignItems: "center", justifyContent: "center", padding: "1rem", backdropFilter: "blur(4px)" }} onClick={() => setPlaying(null)}>
          <div style={{ background: "#14141f", borderRadius: 16, maxWidth: 700, width: "100%", border: "1px solid rgba(255,255,255,0.1)", overflow: "hidden" }} onClick={e => e.stopPropagation()}>
            <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", padding: "1rem 1.2rem 0.5rem" }}>
              <h3 style={{ margin: 0, fontSize: "1.05rem" }}>🎬 {playing.title}</h3>
              <button onClick={() => setPlaying(null)} style={{ background: "rgba(255,255,255,0.1)", border: "none", color: "#fff", borderRadius: "50%", width: 30, height: 30, cursor: "pointer", fontSize: "1rem" }}>✕</button>
            </div>
            <video src={playing.url} controls autoPlay style={{ width: "100%", maxHeight: 360, background: "#000" }} />
            <div style={{ padding: "1rem 1.2rem 1.2rem" }}>
              {/* Movie Info */}
              <div style={{ display: "flex", gap: 8, flexWrap: "wrap", marginBottom: 8 }}>
                <span style={{ background: "rgba(229,9,20,0.18)", color: "#e50914", borderRadius: 4, padding: "2px 10px", fontSize: "0.78rem", fontWeight: 700 }}>{playing.genre}</span>
                <span style={{ background: "rgba(255,255,255,0.07)", color: "#aaa", borderRadius: 4, padding: "2px 10px", fontSize: "0.78rem" }}>{playing.year}</span>
                <span style={{ color: "#f5c518", fontSize: "0.82rem", fontWeight: 700 }}>⭐ {playing.rating}</span>
                <span style={{ color: "#777", fontSize: "0.78rem" }}>👁 {playing.views} views</span>
              </div>
              <p style={{ color: "#aaa", fontSize: "0.88rem", margin: "0 0 12px" }}>{playing.description}</p>
              {/* Buttons */}
              <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
                <button style={{ background: "#e50914", color: "#fff", border: "none", borderRadius: 6, padding: "9px 16px", fontWeight: 700, cursor: "pointer", display: "flex", alignItems: "center", gap: 6 }} onClick={copyLink}>{t.shareBtn}</button>
                {/* Download Button */}
                <a
                  href={playing.url}
                  download={playing.title + ".mp4"}
                  onClick={() => showToast("⬇️ " + (t.downloadStart || "Download shuru ho gaya!"))}
                  style={{ background: "linear-gradient(135deg,#1a6b1a,#0f4f0f)", color: "#fff", border: "none", borderRadius: 6, padding: "9px 16px", fontWeight: 700, cursor: "pointer", textDecoration: "none", display: "flex", alignItems: "center", gap: 6, fontSize: "0.9rem" }}>
                  ⬇️ {t.downloadBtn || "Download"}
                </a>
                <button style={{ background: "transparent", color: "#f0f0f0", border: "1px solid rgba(255,255,255,0.2)", borderRadius: 6, padding: "9px 16px", fontWeight: 600, cursor: "pointer" }} onClick={() => setPlaying(null)}>{t.backBtn}</button>
              </div>
            </div>
          </div>
        </div>
      )}

      {/* Upload Modal */}
      {showUpload && (
        <div style={{ position: "fixed", inset: 0, background: "rgba(0,0,0,0.88)", zIndex: 200, display: "flex", alignItems: "center", justifyContent: "center", padding: "1rem", backdropFilter: "blur(4px)" }} onClick={() => setShowUpload(false)}>
          <div style={{ background: "#14141f", borderRadius: 16, maxWidth: 500, width: "100%", border: "1px solid rgba(255,255,255,0.1)", overflow: "hidden" }} onClick={e => e.stopPropagation()}>
            <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", padding: "1rem 1.2rem 0.5rem" }}>
              <h3 style={{ margin: 0 }}>🎬 {t.uploadTitle}</h3>
              <button onClick={() => setShowUpload(false)} style={{ background: "rgba(255,255,255,0.1)", border: "none", color: "#fff", borderRadius: "50%", width: 30, height: 30, cursor: "pointer" }}>✕</button>
            </div>
            <div style={{ padding: "0.5rem 1.2rem 1.2rem" }}>
              <label style={{ fontSize: "0.8rem", color: "#aaa", marginBottom: 4, display: "block" }}>{t.movieTitle}</label>
              <input style={fInputStyle} placeholder={t.movieTitlePlaceholder} value={uploadForm.title} onChange={e => setUploadForm(p => ({ ...p, title: e.target.value }))} />
              <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10 }}>
                <div>
                  <label style={{ fontSize: "0.8rem", color: "#aaa", marginBottom: 4, display: "block" }}>{t.genre}</label>
                  <select style={{ ...fInputStyle, cursor: "pointer" }} value={uploadForm.genre} onChange={e => setUploadForm(p => ({ ...p, genre: e.target.value }))}>
                    {GENRES.filter(g => g !== "All").map(g => <option key={g} value={g}>{g}</option>)}
                  </select>
                </div>
                <div>
                  <label style={{ fontSize: "0.8rem", color: "#aaa", marginBottom: 4, display: "block" }}>{t.year}</label>
                  <input style={fInputStyle} placeholder="2024" type="number" value={uploadForm.year} onChange={e => setUploadForm(p => ({ ...p, year: e.target.value }))} />
                </div>
              </div>
              <label style={{ fontSize: "0.8rem", color: "#aaa", marginBottom: 4, display: "block" }}>{t.description}</label>
              <textarea style={{ ...fInputStyle, minHeight: 65, resize: "vertical" }} placeholder={t.descPlaceholder} value={uploadForm.description} onChange={e => setUploadForm(p => ({ ...p, description: e.target.value }))} />
              <div style={{ border: "2px dashed rgba(229,9,20,0.35)", borderRadius: 10, padding: "1.5rem", textAlign: "center", background: "rgba(229,9,20,0.04)", cursor: "pointer", margin: "8px 0" }} onClick={() => fileRef.current.click()}>
                <div style={{ fontSize: "1.8rem" }}>{uploadForm.file ? "✅" : "🎞️"}</div>
                <div style={{ fontWeight: 600, marginTop: 4, fontSize: "0.9rem" }}>{uploadForm.file ? uploadForm.file.name : t.selectVideo}</div>
                <div style={{ color: "#666", fontSize: "0.78rem" }}>{t.videoSupport}</div>
                <input ref={fileRef} type="file" accept="video/*" hidden onChange={e => setUploadForm(p => ({ ...p, file: e.target.files[0] }))} />
              </div>
              <div style={{ border: "2px dashed rgba(255,255,255,0.1)", borderRadius: 10, padding: "0.9rem", textAlign: "center", cursor: "pointer", marginBottom: 10 }} onClick={() => thumbRef.current.click()}>
                <div style={{ fontSize: "0.88rem", color: "#888" }}>{uploadForm.thumb ? "🖼️ ✅ " + uploadForm.thumb.name : "🖼️ " + t.thumbnail}</div>
                <input ref={thumbRef} type="file" accept="image/*" hidden onChange={e => setUploadForm(p => ({ ...p, thumb: e.target.files[0] }))} />
              </div>
              <button style={{ background: "#e50914", color: "#fff", border: "none", borderRadius: 8, padding: "12px", width: "100%", fontWeight: 700, fontSize: "1rem", cursor: "pointer", opacity: uploading ? 0.7 : 1 }} onClick={handleUpload} disabled={uploading}>
                {uploading ? t.uploading : t.uploadBtn}
              </button>
            </div>
          </div>
        </div>
      )}

      {/* Footer */}
      <footer style={{ textAlign: "center", padding: "1.8rem", color: "#444", fontSize: "0.8rem", borderTop: "1px solid rgba(255,255,255,0.05)", marginTop: "2rem" }}>
        🎬 {t.footerText}
      </footer>

      <style>{`*{box-sizing:border-box}::-webkit-scrollbar{width:6px;height:6px}::-webkit-scrollbar-track{background:#0a0a0f}::-webkit-scrollbar-thumb{background:#e50914;border-radius:3px}@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}select option{background:#1e1e2e}`}</style>
    </div>
  );
}

// ─── Small Components ─────────────────────────────────────────────────────────
const fInputStyle = { background: "rgba(255,255,255,0.06)", border: "1px solid rgba(255,255,255,0.14)", borderRadius: 8, padding: "10px 13px", color: "#fff", fontSize: "0.93rem", width: "100%", outline: "none", boxSizing: "border-box", marginBottom: 10 };
const btnStyle = { background: "linear-gradient(135deg,#e50914,#c0060f)", color: "#fff", border: "none", borderRadius: 9, padding: "12px", width: "100%", fontWeight: 700, fontSize: "1rem", cursor: "pointer", marginTop: 4 };

function AuthInput({ label, placeholder, type = "text", value, onChange }) {
  return (
    <div style={{ marginBottom: 12 }}>
      <label style={{ fontSize: "0.8rem", color: "#aaa", marginBottom: 5, display: "block" }}>{label}</label>
      <input type={type} placeholder={placeholder} value={value} onChange={e => onChange(e.target.value)}
        style={{ background: "rgba(255,255,255,0.06)", border: "1px solid rgba(255,255,255,0.13)", borderRadius: 9, padding: "11px 14px", color: "#fff", fontSize: "0.95rem", width: "100%", outline: "none", boxSizing: "border-box" }} />
    </div>
  );
}

function Divider({ label }) {
  return (
    <div style={{ display: "flex", alignItems: "center", gap: 10, margin: "16px 0" }}>
      <div style={{ flex: 1, height: 1, background: "rgba(255,255,255,0.08)" }} />
      <span style={{ color: "#555", fontSize: "0.82rem" }}>{label}</span>
      <div style={{ flex: 1, height: 1, background: "rgba(255,255,255,0.08)" }} />
    </div>
  );
}

function GoogleBtn({ label, onClick }) {
  return (
    <button onClick={onClick} style={{ background: "#fff", color: "#333", border: "none", borderRadius: 9, padding: "11px", width: "100%", fontWeight: 700, fontSize: "0.92rem", cursor: "pointer", display: "flex", alignItems: "center", justifyContent: "center", gap: 10 }}>
      <svg width="18" height="18" viewBox="0 0 24 24">
        <path d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" fill="#4285F4"/>
        <path d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" fill="#34A853"/>
        <path d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" fill="#FBBC05"/>
        <path d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" fill="#EA4335"/>
      </svg>
      {label}
    </button>
  );
}
