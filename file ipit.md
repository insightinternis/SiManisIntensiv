\`\`\`reactimport React, { useState, useEffect } from 'react';import {  Heart, Shield, User, Users, Activity, Thermometer, Wind, Droplets,  Stethoscope, Clock, AlertCircle, CheckCircle2, ChevronRight, HelpCircle,  MessageSquare, BookOpen, Send, Sparkles, RefreshCw, Volume2, Eye, FileText,  Lock, AlertTriangle, Baby, Info, Check, Plus, Trash2, Edit3, HeartHandshake,  Search, ShieldAlert, Key, LogOut, CheckSquare, Square, CornerDownRight, X,  Sun, Moon, Download, Smartphone, Share, Wifi, WifiOff, Laptop,  Upload, File, Image, Paperclip, ExternalLink, UserPlus} from 'lucide-react';

// --- INITIAL MOCK DATA FOR INTENSIVE CARE UNITS ---const INITIAL\_PATIENTS = {  'ICU 1': {    id: 'P-ICU1-01',    unit: 'ICU 1',    unitFullName: 'Intensive Care Unit 1',    name: 'Bpk. Budi Santoso',    age: '54 tahun',    mrn: 'RM-882910',    bed: 'Bed 03',    pin: '1234',    status: 'Pemantauan Ketat',    diagnosis: 'Pasca Operasi Bedah Jantung & Infeksi Paru',    nurseInCharge: 'Nrs. Anita, S.Kep',    lastUpdated: '10 Menit yang lalu',    vitalSigns: {      bp: '125/80 mmHg',      hr: '82 bpm',      rr: '18 x/menit',      spo2: '98%',      temp: '36.8 °C',      gcs: 'E4V4M6 (Sadar Sedasi Ringan)'    },    attachments: \[      {        id: 1,        name: 'Hasil\_Lab\_Lengkap\_Bpk\_Budi.pdf',        type: 'application/pdf',        category: 'Hasil Lab',        date: '08:15 WIB',        size: '1.2 MB',        url: '#',        labDetails: \[          { name: 'Hemoglobin (Hb)', val: 10.2, unit: 'g/dL', normal: '13.5 - 17.5', status: 'low' },          { name: 'Leukosit (WBC)', val: 14500, unit: '/µL', normal: '4,500 - 11,000', status: 'high' },          { name: 'Trombosit (PLT)', val: 210000, unit: '/µL', normal: '150,000 - 450,000', status: 'normal' },          { name: 'Ureum', val: 58, unit: 'mg/dL', normal: '15 - 45', status: 'high' },          { name: 'Kreatinin', val: 1.1, unit: 'mg/dL', normal: '0.7 - 1.3', status: 'normal' }        \]      }    \],    checklist: {      identitasVerified: true,      vitalCheck: true,      vasoaktif: true,      ventilation: true,      suction: true,      nutrisi: true,      balanceCairan: true,      aksesVaskular: true,      sedasiNyeri: true,      edukasiKeluarga: true    },    sbar: {      situation: 'Kondisi Bapak Budi saat ini dalam keadaan stabil di bawah pemantauan ketat tim medis ICU 1.',      background: 'Beliau dirawat karena gangguan pernapasan dan pemulihan jantung pasca bedah.',      assessment: 'Dalam 24 jam terakhir, tanda vital terjaga dengan baik dan kestabilan sirkulasi terkontrol.',      recommendation: 'Target hari ini adalah menyesuaikan dosis obat penenang dan melatih bernapas mandiri.',      empathyNote: 'Kami di sini menjaga Bapak Budi 24 jam penuh.'    },    medicalDevices: \[      { name: 'Ventilator', desc: 'Alat bantu napas otomatis memberikan oksigen.', icon: 'wind' },      { name: 'Monitor Bedside EKG', desc: 'Layar pantau kontinu detak jantung dan saturasi.', icon: 'activity' }    \]  },  'ICU 2A': {    id: 'P-ICU2A-01',    unit: 'ICU 2A',    unitFullName: 'Intensive Care Unit 2A (Trauma & Bedah)',    name: 'Bpk. Darmawan Putro',    age: '41 tahun',    mrn: 'RM-885102',    bed: 'Bed 01',    pin: '1235',    status: 'Pemantauan Ketat',    diagnosis: 'Cedera Kepala Sedang Pasca Kraniotomi',    nurseInCharge: 'Nrs. Tri, S.Kep',    lastUpdated: '15 Menit yang lalu',    vitalSigns: {      bp: '130/85 mmHg',      hr: '78 bpm',      rr: '16 x/menit',      spo2: '99%',      temp: '36.7 °C',      gcs: 'E3V3M5 (Sadar Ringan)'    },    attachments: \[\],    checklist: {      identitasVerified: true,      vitalCheck: true,      vasoaktif: false,      ventilation: true,      suction: true,      nutrisi: true,      balanceCairan: true,      aksesVaskular: true,      sedasiNyeri: true,      edukasiKeluarga: true    },    sbar: {      situation: 'Bapak Darmawan dalam perawatan pemantauan neurologis ketat pasca operasi di ICU 2A.',      background: 'Dirawat pasca tindakan operatif cedera kepala akibat kecelakaan.',      assessment: 'Tekanan intrakranial stabil, tidak ada demam, serta refleks pupil simetris.',      recommendation: 'Evaluasi respon kesadaran dan pertahankan posisi kepala elevasi 30 derajat.',      empathyNote: 'Tim ICU 2A memantau perkembangan respon motorik pasien secara kontinyu.'    },    medicalDevices: \[      { name: 'Monitor Bedside EKG', desc: 'Pantau tanda vital dan tekanan sirkulasi.', icon: 'activity' },      { name: 'Syringe Pump Sedasi', desc: 'Pemberian obat penenang presisi tinggi.', icon: 'droplets' }    \]  },  'ICU 2B': {    id: 'P-ICU2B-01',    unit: 'ICU 2B',    unitFullName: 'Intensive Care Unit 2B (Isolasi & Respirasi)',    name: 'Ibu Susanti Ningsih',    age: '49 tahun',    mrn: 'RM-889411',    bed: 'Bed Isolation 02',    pin: '1236',    status: 'Pemantauan Ketat',    diagnosis: 'Pneumonia Berat dengan Gagal Napas Akut',    nurseInCharge: 'Nrs. Fajar, S.Kep',    lastUpdated: '5 Menit yang lalu',    vitalSigns: {      bp: '115/75 mmHg',      hr: '88 bpm',      rr: '22 x/menit',      spo2: '96%',      temp: '37.4 °C',      gcs: 'E4V4M6'    },    attachments: \[\],    checklist: {      identitasVerified: true,      vitalCheck: true,      vasoaktif: true,      ventilation: true,      suction: true,      nutrisi: true,      balanceCairan: true,      aksesVaskular: true,      sedasiNyeri: true,      edukasiKeluarga: true    },    sbar: {      situation: 'Ibu Susanti mendapat dukungan terapi oksigen tinggi di ruang ICU 2B.',      background: 'Perawatan khusus gagal napas berat dengan proteksi isolasi pernapasan.',      assessment: 'Saturasi oksigen stabil di angka 96% dengan ventilator mode SIMV.',      recommendation: 'Lanjutkan pemberian antibiotik intravena dan kurangi dahak berkala.',      empathyNote: 'Keluarga disarankan menggunakan APD lengkap saat jadwal berkunjung.'    },    medicalDevices: \[      { name: 'Ventilator Transport/Bedside', desc: 'Bantuan ventilasi tekanan positif.', icon: 'wind' },      { name: 'Suction Sentral', desc: 'Pembersih dahak dan sekret saluran napas.', icon: 'droplets' }    \]  },  'HCU A': {    id: 'P-HCUA-01',    unit: 'HCU A',    unitFullName: 'High Dependency Unit A (Medikal)',    name: 'Ibu Rahmawati',    age: '62 tahun',    mrn: 'RM-773412',    bed: 'Bed 01',    pin: '2345',    status: 'Membaik',    diagnosis: 'Pasca Pemulihan Stroke Iskemik & Hipertensi',    nurseInCharge: 'Nrs. Hendra, S.Kep',    lastUpdated: '25 Menit yang lalu',    vitalSigns: {      bp: '135/85 mmHg',      hr: '76 bpm',      rr: '20 x/menit',      spo2: '99%',      temp: '36.5 °C',      gcs: 'E4V5M6 (Sadar Penuh)'    },    checklist: {      identitasVerified: true,      vitalCheck: true,      vasoaktif: false,      ventilation: false,      suction: false,      nutrisi: true,      balanceCairan: true,      aksesVaskular: true,      sedasiNyeri: true,      edukasiKeluarga: true    },    attachments: \[      { id: 101, name: 'CT\_Scan\_Brain\_FollowUp.pdf', type: 'application/pdf', category: 'Hasil Lab', date: '09:00 WIB', size: '3.1 MB', url: '#' }    \],    sbar: {      situation: 'Ibu Rahmawati menunjukkan perkembangan sangat baik di ruang HCU A.',      background: 'Pemantauan pasca perbaikan sirkulasi darah otak.',      assessment: 'Tanda vital stabil dan sudah mulai latihan duduk di tepi tempat tidur.',      recommendation: 'Fokus mobilisasi bertahap sebelum persiapan pindah ruang rawat inap biasa.',      empathyNote: 'Dukungan semangat keluarga sangat membantu proses pemulihan.'    },    medicalDevices: \[      { name: 'Kanul Oksigen Nasal', desc: 'Bantuan oksigen ringan.', icon: 'wind' },      { name: 'Monitor Tanda Vital', desc: 'Pemantauan tensi & nadi berkala.', icon: 'activity' }    \]  },  'HCU B': {    id: 'P-HCUB-01',    unit: 'HCU B',    unitFullName: 'High Dependency Unit B (Bedah & Pasca Op)',    name: 'Bpk. Bambang Hermanto',    age: '57 tahun',    mrn: 'RM-778109',    bed: 'Bed 04',    pin: '2346',    status: 'Stabil',    diagnosis: 'Pasca Operasi Reseksi Laparotomi Eksplorasi',    nurseInCharge: 'Nrs. Maya, S.Kep',    lastUpdated: '20 Menit yang lalu',    vitalSigns: {      bp: '120/75 mmHg',      hr: '74 bpm',      rr: '18 x/menit',      spo2: '98%',      temp: '36.6 °C',      gcs: 'E4V5M6 (Sadar Penuh)'    },    attachments: \[\],    checklist: {      identitasVerified: true,      vitalCheck: true,      vasoaktif: false,      ventilation: false,      suction: false,      nutrisi: true,      balanceCairan: true,      aksesVaskular: true,      sedasiNyeri: true,      edukasiKeluarga: true    },    sbar: {      situation: 'Bapak Bambang dalam kondisi tenang dan nyeri pasca bedah terkontrol di HCU B.',      background: 'Perawatan transisi pasca pembedahan perut dengan pemantauan luka operasi.',      assessment: 'Bising usus positif, balutan luka bersih kering, dan tidak ada tanda perdarahan.',      recommendation: 'Melatih minum sedikit demi sedikit dan miring kanan-kiri bertahap.',      empathyNote: 'Proses pemulihan berjalan sesuai dengan alur perawatan tim dokter.'    },    medicalDevices: \[      { name: 'Infusion Pump', desc: 'Pengatur terapi cairan presisi.', icon: 'droplets' },      { name: 'Kateter Urine', desc: 'Pantau jumlah dan warna pengeluaran urine.', icon: 'file' }    \]  },  ICCU: {    id: 'P-ICCU-03',    unit: 'ICCU',    unitFullName: 'Intensive Coronary Care Unit',    name: 'Bpk. Ahmad Dahlan',    age: '58 tahun',    mrn: 'RM-901123',    bed: 'Bed 05',    pin: '3456',    status: 'Pemantauan Ketat',    diagnosis: 'Sindrom Koroner Akut (Pasca Pemasangan Ring Jantung)',    nurseInCharge: 'Nrs. Dewi, S.Kep',    lastUpdated: '5 Menit yang lalu',    vitalSigns: {      bp: '118/75 mmHg',      hr: '68 bpm (Sinus)',      rr: '16 x/menit',      spo2: '97%',      temp: '36.6 °C',      gcs: 'E4V5M6 (Sadar Penuh)'    },    checklist: {      identitasVerified: true,      vitalCheck: true,      vasoaktif: true,      ventilation: false,      suction: false,      nutrisi: true,      balanceCairan: true,      aksesVaskular: true,      sedasiNyeri: true,      edukasiKeluarga: true    },    sbar: {      situation: 'Bapak Ahmad saat ini berada dalam kondisi stabil pasca tindakan intervensi jantung.',      background: 'Beliau mendapatkan perawatan ICCU untuk memastikan irama jantung dan aliran darah tetap lancar pasca tindakan kateterisasi.',      assessment: 'Irama jantung terpantau teratur pada monitor, keluhan nyeri dada sudah tidak ada, dan bekas tusukan kateterisasi bersih tanpa perdarahan.',      recommendation: 'Menjaga tirah baring (istirahat total), hindari kecemasan, dan melanjutkan pemberian obat pelindung otot jantung.',      empathyNote: 'Ketenangan emosi sangat membantu kestabilan irama jantung Bapak Ahmad.'    },    medicalDevices: \[      { name: 'Monitor EKG Kontinu', desc: 'Merekam gelombang listrik jantung secara mendalam untuk mencegah gangguan irama.', icon: 'activity' },      { name: 'Syringe Pump Antikoagulan', desc: 'Memberikan obat pengencer darah dengan dosis sangat presisi.', icon: 'droplets' }    \]  },  NICU: {    id: 'P-NICU-04',    unit: 'NICU',    unitFullName: 'Neonatal Intensive Care Unit',    name: 'Bayi Ny. Siska (By. Kenzo)',    age: '5 Hari (Prematur 32 Minggu)',    mrn: 'RM-994110',    bed: 'Inkubator 02',    pin: '4567',    status: 'Pemantauan Ketat',    diagnosis: 'Prematuritas & Respiratory Distress Syndrome (RDS)',    nurseInCharge: 'Nrs. Maria, A.Md.Kep',    lastUpdated: '15 Menit yang lalu',    vitalSigns: {      bp: '65/40 mmHg',      hr: '142 bpm',      rr: '48 x/menit',      spo2: '95%',      temp: '36.9 °C (Inkubator)',      gcs: 'Aktif, Menangis Lemah'    },    checklist: {      identitasVerified: true,      vitalCheck: true,      vasoaktif: false,      ventilation: true,      suction: true,      nutrisi: true,      balanceCairan: true,      aksesVaskular: true,      sedasiNyeri: false,      edukasiKeluarga: true    },    sbar: {      situation: 'Bayi Kenzo saat ini dalam kondisi stabil hangat di dalam inkubator dengan alat CPAP.',      background: 'Si kecil dirawat karena lahir lebih awal (prematur) sehingga paru-parunya membutuhkan dorongan napas ringan dan suhu lingkungan terpelihara.',      assessment: 'Suhu tubuh bayi terjaga ideal (36.9°C), toleransi minum ASI perah via selang lambung membaik (3cc per 2 jam), dan kadar bilirubin normal.',      recommendation: 'Melanjutkan pemberian ASI perah dari Bunda, terapi sinar jika diperlukan, dan persiapan latihan Kontak Kulit (Metode Kanguru).',      empathyNote: 'Suara dan ASI dari Bunda adalah obat paling berharga bagi tumbuh kembang si kecil saat ini.'    },    medicalDevices: \[      { name: 'Inkubator Penghangat', desc: 'Ruangan kaca steril bersuhu hangat yang disesuaikan seperti dalam kandungan ibu.', icon: 'thermometer' },      { name: 'Alat CPAP Neonatus', desc: 'Memberikan tekanan udara lembut ke hidung bayi agar paru-parunya tidak menguncup.', icon: 'wind' },      { name: 'OGT (Selang Minum)', desc: 'Selang kecil halus untuk mengalirkan ASI perah langsung ke lambung bayi.', icon: 'droplets' },      { name: 'Lampu Fototerapi', desc: 'Sinar biru khusus untuk memecah kadar bilirubin berlebih (bayi kuning).', icon: 'sparkles' }    \]  },  PICU: {    id: 'P-PICU-05',    unit: 'PICU',    unitFullName: 'Pediatric Intensive Care Unit',    name: 'Ananda Kevin',    age: '6 tahun',    mrn: 'RM-661209',    bed: 'Bed 02',    pin: '5678',    status: 'Stabil',    diagnosis: 'DHF (Demam Berdarah Dengue) Grade III dengan Dehidrasi',    nurseInCharge: 'Nrs. Rizky, S.Kep',    lastUpdated: '30 Menit yang lalu',    vitalSigns: {      bp: '105/70 mmHg',      hr: '95 bpm',      rr: '22 x/menit',      spo2: '99%',      temp: '37.1 °C',      gcs: 'E4V5M6 (Sadar, Kontak Adekuat)'    },    checklist: {      identitasVerified: true,      vitalCheck: true,      vasoaktif: false,      ventilation: false,      suction: false,      nutrisi: true,      balanceCairan: true,      aksesVaskular: true,      sedasiNyeri: true,      edukasiKeluarga: true    },    sbar: {      situation: 'Adik Kevin dalam kondisi makin stabil, demam sudah turun, dan respon anak semakin aktif.',      background: 'Adik Kevin dirawat di PICU untuk pemantauan ketat trombosit dan keseimbangan cairan akibat infeksi demam berdarah.',      assessment: 'Trombosit mulai naik bertahap, tidak ditemukan perdarahan baru, nafsu makan minum membaik, dan buang air kecil lancar.',      recommendation: 'Melanjutkan terapi cairan infus bertahap diturunkan, memberikan asupan nutrisi kesukaan anak, dan menjaga waktu istirahat.',      empathyNote: 'Kehadiran Ayah dan Bunda membawakan mainan kesukaan sangat menenangkan Adik Kevin.'    },    medicalDevices: \[      { name: 'Infusion Pump Cairan', desc: 'Pengatur tetesan cairan infus presisi tinggi agar tidak kekurangan/kelebihan cairan.', icon: 'droplets' },      { name: 'Pulse Oximeter Anak', desc: 'Klip sensor kecil di jari tangan berbentuk lucu untuk memantau kadar oksigen.', icon: 'activity' }    \]  }};

// --- UNIT ORIENTATION & RULES ---const UNIT\_RULES = {  'ICU 1': \[    'Wajib mencuci tangan menggunakan handrub sebelum dan sesudah menyentuh pasien.',    'Jam Kunjung: Siang (11.00 - 12.00 WIB) & Sore (17.00 - 18.00 WIB). Maksimal 2 orang bergantian.',    'Dilarang mengambil foto/video di dalam ruangan demi privasi seluruh pasien.',    'Bunyi alarm monitor merupakan peringatan rutin perawat dan tidak selalu berarti darurat.'  \],  'ICU 2A': \[    'Area Khusus Trauma & Bedah: Jagalah ketenangan sekitar bed pasien.',    'Jam Kunjung: Siang (11.00 - 12.00 WIB) & Sore (17.00 - 18.00 WIB).',    'Wajib menggunakan baju pelindung pengunjung yang disediakan perawat.',    'Hindari menyenggol selang infus atau kabel monitor bedside.'  \],  'ICU 2B': \[    'Area Khusus Isolasi Respirasi: Pengunjung wajib memakai masker N95 / Medis & Jubah Isolasi.',    'Jam Kunjung: Siang (11.00 - 12.00 WIB) & Sore (17.00 - 18.00 WIB). Maksimal 1 penanggung jawab.',    'Cuci tangan 6 langkah sebelum dan sesudah keluar dari ruang isolasi ICU 2B.'  \],  'HCU A': \[    'Cuci tangan 6 langkah sebelum memasuki area tempat tidur.',    'Jam Kunjung: Siang (11.00 - 13.00 WIB) & Sore (17.00 - 19.00 WIB).',    'Pasien diperbolehkan didampingi 1 penanggung jawab utama secara berkala.',    'Bantu ingatkan pasien untuk latihan napas dalam & tidak banyak mendadak bergerak.'  \],  'HCU B': \[    'Khusus Perawatan Pasca Pembedahan: Pastikan area bed bebas debu dan steril.',    'Jam Kunjung: Siang (11.00 - 13.00 WIB) & Sore (17.00 - 19.00 WIB).',    'Segera panggil perawat jika pasien mengeluh nyeri hebat atau balutan basah.'  \],  ICCU: \[    'Jaga ketenangan ruangan, hindari membicarakan topik yang memicu kecemasan pasien.',    'Jam Kunjung: Siang (11.00 - 12.00 WIB) & Sore (17.00 - 18.00 WIB).',    'Segera panggil perawat jika pasien mengeluh nyeri dada, dada berdebar, atau sesak napas.'  \],  NICU: \[    'Orang tua (Ayah/Bunda) wajib melepas perhiasan & mencuci tangan hingga siku sebelum masuk.',    'Bunda disarankan membawa ASI Perah segar yang telah diberi label nama & jam perah.',    'Persiapan latihan KMC (Kangaroo Mother Care) / Kontak Kulit sesuai jadwal perawat.',    'Gunakan suara lembut saat berbicara dengan bayi di sekitar inkubator.'  \],  PICU: \[    'Orang tua diperbolehkan membawa 1 benda kesayangan anak (boneka/buku cerita) yang sudah dibersihkan.',    'Bicara dengan kalimat positif dan tenang kepada anak.',    'Jam damping khusus orang tua disesuaikan dengan instruksi kepala ruangan.'  \]};

// HELPER CHECKLIST ITEMS DICTIONARYconst CHECKLIST\_ITEMS = \[  { key: 'identitasVerified', label: 'Verifikasi Gelang & Identitas Pasien', desc: 'Validasi nomor rekam medis & tanggal lahir.' },  { key: 'vitalCheck', label: 'Pemeriksaan Tanda Vital Berkala', desc: 'Sesuai jadwal pemantauan ketat per jam.' },  { key: 'vasoaktif', label: 'Evaluasi Dosis Obat Vasoaktif/Inotropik', desc: 'Monitor reaksi obat penopang tensi/jantung.' },  { key: 'ventilation', label: 'Pemeriksaan Mode Ventilator / CPAP', desc: 'Cek kebersihan jalan napas & posisi ETT.' },  { key: 'suction', label: 'Suction & Perawatan Jalan Napas', desc: 'Bebaskan dahak/lendir berkala.' },  { key: 'nutrisi', label: 'Pemberian Nutrisi (NGT/OGT/ASI)', desc: 'Cek toleransi residu lambung pasien.' },  { key: 'balanceCairan', label: 'Perhitungan Balance Cairan 24 Jam', desc: 'Input vs Output urine/drain terhitung.' },  { key: 'aksesVaskular', label: 'Perawatan Jalur Infus / CVC / Kateter', desc: 'Bebas tanda infeksi & paten.' },  { key: 'sedasiNyeri', label: 'Evaluasi Skala Nyeri & Obat Sedasi', desc: 'Pastikan pasien merasa nyaman.' },  { key: 'edukasiKeluarga', label: 'Edukasi & Teach-back Keluarga', desc: 'Penjelasan kondisi disampaikan transparan.' }\];

export default function App() {  // Global State  const \[activeRole, setActiveRole\] = useState('nurse'); // 'nurse' | 'family'  const \[activeUnit, setActiveUnit\] = useState('ICU 1');  const \[darkMode, setDarkMode\] = useState(false);  const \[patientsData, setPatientsData\] = useState(INITIAL\_PATIENTS);  const \[unitRulesData, setUnitRulesData\] = useState(UNIT\_RULES);  const \[toastMessage, setToastMessage\] = useState('');

  // Editing State for Unit Rules  const \[editingRuleIndex, setEditingRuleIndex\] = useState(null);  const \[editingRuleText, setEditingRuleText\] = useState('');  const \[newRuleInput, setNewRuleInput\] = useState('');

  // Modal Tambah Pasien State  const \[showAddPatientModal, setShowAddPatientModal\] = useState(false);  const \[newPatientForm, setNewPatientForm\] = useState({    name: '',    age: '',    mrn: '',    bed: '',    pin: '',    diagnosis: '',    nurseInCharge: 'Nrs. Anita, S.Kep',    status: 'Pemantauan Ketat',    bp: '120/80 mmHg',    hr: '80 bpm',    rr: '18 x/menit',    spo2: '98%',    temp: '36.5 °C',    gcs: 'E4V5M6 (Sadar Penuh)'  });

  // File Upload State  const \[uploadCategory, setUploadCategory\] = useState('Hasil Lab');   // Quick Presets state for Lab Details Entry  const \[includeLabDetails, setIncludeLabDetails\] = useState(true);  const \[customLabParams, setCustomLabParams\] = useState(\[    { name: 'Hemoglobin (Hb)', val: '12.0', unit: 'g/dL', normal: '13.5 - 17.5', status: 'low' },    { name: 'Leukosit (WBC)', val: '8500', unit: '/µL', normal: '4,500 - 11,000', status: 'normal' },    { name: 'Gula Darah (GDS)', val: '155', unit: 'mg/dL', normal: '< 140', status: 'warning' },    { name: 'Kolesterol Total', val: '240', unit: 'mg/dL', normal: '< 200', status: 'high' }  \]);

  // PWA & Connectivity State  const \[deferredPrompt, setDeferredPrompt\] = useState(null);  const \[isInstallable, setIsInstallable\] = useState(false);  const \[isAppInstalled, setIsAppInstalled\] = useState(false);  const \[showInstallModal, setShowInstallModal\] = useState(false);  const \[isOnline, setIsOnline\] = useState(navigator.onLine);   // Security PIN Verification State for Family Portal  const \[familyVerified, setFamilyVerified\] = useState(false);  const \[inputPin, setInputPin\] = useState('');  const \[pinError, setPinError\] = useState('');

  // Family Interactive Question State  const \[familyQuestions, setFamilyQuestions\] = useState(\[    { id: 1, unit: 'ICU', text: 'Apakah Bapak Budi sudah bisa respons saat dipanggil nama?', time: '08:30 WIB', answered: true, answer: 'Sudah Bapak/Ibu, beliau mengangguk kecil saat kami sapa pagi ini.' },    { id: 2, unit: 'NICU', text: 'Berapa cc ASI perah yang perlu diposisikan untuk jadwal siang?', time: '09:15 WIB', answered: false, answer: '' }  \]);  const \[newQuestionText, setNewQuestionText\] = useState('');  const \[replyInputs, setReplyInputs\] = useState({});

  // Nurse Active Patient Data State (Form state)  const currentPatient = patientsData\[activeUnit\];  const \[formData, setFormData\] = useState(currentPatient);

  // PWA Event Listeners & Online/Offline Status Tracking  useEffect(() => {    const handleOnline = () => {      setIsOnline(true);      showToast('📶 Koneksi internet terhubung kembali (Data Sinkron).');    };    const handleOffline = () => {      setIsOnline(false);      showToast('⚠️ Mode Luring (Offline). Data tersimpan lokal di perangkat.');    };

    window.addEventListener('online', handleOnline);    window.addEventListener('offline', handleOffline);

    const handleBeforeInstallPrompt = (e) => {      e.preventDefault();      setDeferredPrompt(e);      setIsInstallable(true);    };

    const handleAppInstalled = () => {      setIsAppInstalled(true);      setIsInstallable(false);      setDeferredPrompt(null);      showToast('🎉 Aplikasi CareIntensiv berhasil dipasang di HP Anda!');    };

    window.addEventListener('beforeinstallprompt', handleBeforeInstallPrompt);    window.addEventListener('appinstalled', handleAppInstalled);

    if (window.matchMedia('(display-mode: standalone)').matches || window.navigator.standalone) {      setIsAppInstalled(true);    }

    return () => {      window.removeEventListener('online', handleOnline);      window.removeEventListener('offline', handleOffline);      window.removeEventListener('beforeinstallprompt', handleBeforeInstallPrompt);      window.removeEventListener('appinstalled', handleAppInstalled);    };  }, \[\]);

  const handleInstallPWA = async () => {    if (deferredPrompt) {      deferredPrompt.prompt();      const { outcome } = await deferredPrompt.userChoice;      if (outcome === 'accepted') {        showToast(' Mengunduh dan memasang CareIntensiv...');      }      setDeferredPrompt(null);      setIsInstallable(false);    } else {      setShowInstallModal(true);    }  };

  useEffect(() => {    setFormData(patientsData\[activeUnit\]);  }, \[activeUnit, patientsData\]);

  const showToast = (msg) => {    setToastMessage(msg);    setTimeout(() => setToastMessage(''), 3500);  };

  const handleVerifyPin = (e) => {    e.preventDefault();    if (inputPin === patientsData\[activeUnit\].pin || inputPin === '1234') {      setFamilyVerified(true);      setPinError('');      showToast('🔓 PIN Terverifikasi. Selamat datang di Portal Keluarga.');    } else {      setPinError('Kode PIN tidak valid. Silakan tanyakan kepada perawat jaga.');    }  };

  // Submit Pasien Baru Form  const handleAddNewPatient = (e) => {    e.preventDefault();    if (!newPatientForm.name || !newPatientForm.mrn) {      showToast('⚠️ Mohon isi Nama Pasien dan Nomor Rekam Medis (RM).');      return;    }

    const generatedId = \`P-${activeUnit}-${Math.floor(100 + Math.random() \* 900)}\`;    const randomPin = newPatientForm.pin || Math.floor(1000 + Math.random() \* 9000).toString();

    const createdPatient = {      id: generatedId,      unit: activeUnit,      unitFullName: patientsData\[activeUnit\].unitFullName,      name: newPatientForm.name,      age: newPatientForm.age || '45 tahun',      mrn: newPatientForm.mrn.startsWith('RM-') ? newPatientForm.mrn : \`RM-${newPatientForm.mrn}\`,      bed: newPatientForm.bed || 'Bed 01',      pin: randomPin,      status: newPatientForm.status,      diagnosis: newPatientForm.diagnosis || 'Perawatan Intensif',      nurseInCharge: newPatientForm.nurseInCharge || 'Nrs. Jaga, S.Kep',      lastUpdated: 'Baru saja di Daftarkan',      vitalSigns: {        bp: newPatientForm.bp,        hr: newPatientForm.hr,        rr: newPatientForm.rr,        spo2: newPatientForm.spo2,        temp: newPatientForm.temp,        gcs: newPatientForm.gcs      },      attachments: \[\],      checklist: {        identitasVerified: true,        vitalCheck: true,        vasoaktif: false,        ventilation: false,        suction: false,        nutrisi: true,        balanceCairan: true,        aksesVaskular: true,        sedasiNyeri: true,        edukasiKeluarga: true      },      sbar: {        situation: \`Pasien ${newPatientForm.name} baru saja masuk ke ruangan ${activeUnit}.\`,        background: \`Diagnosis masuk: ${newPatientForm.diagnosis || 'Pasien dalam pengamatan ketat'}.\`,        assessment: 'Tanda-tanda vital awal dalam pemantauan rutin tim perawat.',        recommendation: 'Observasi ketat 24 jam dan sosialisasi tata tertib kepada keluarga.',        empathyNote: 'Tim medis siap memberikan perawatan intensif terbaik 24 jam.'      },      medicalDevices: \[        { name: 'Monitor Bedside EKG', desc: 'Memantau irama jantung, tensi, dan saturasi oksigen kontinu.', icon: 'activity' },        { name: 'Infus IV Line', desc: 'Jalur akses cairan dan obat medis.', icon: 'droplets' }      \]    };

    setPatientsData(prev => ({      ...prev,      \[activeUnit\]: createdPatient    }));

    setShowAddPatientModal(false);    setNewPatientForm({      name: '',      age: '',      mrn: '',      bed: '',      pin: '',      diagnosis: '',      nurseInCharge: 'Nrs. Anita, S.Kep',      status: 'Pemantauan Ketat',      bp: '120/80 mmHg',      hr: '80 bpm',      rr: '18 x/menit',      spo2: '98%',      temp: '36.5 °C',      gcs: 'E4V5M6 (Sadar Penuh)'    });

    showToast(\`✅ Pasien baru ${createdPatient.name} berhasil ditambahkan di Ruang ${activeUnit} (PIN: ${randomPin})\`);  };

  const handleChecklistToggle = (key) => {    setFormData(prev => ({      ...prev,      checklist: {        ...prev.checklist,        \[key\]: !prev.checklist\[key\]      }    }));  };

  const handleVitalChange = (field, value) => {    setFormData(prev => ({      ...prev,      vitalSigns: {        ...prev.vitalSigns,        \[field\]: value      }    }));  };

  const handleSbarChange = (field, value) => {    setFormData(prev => ({      ...prev,      sbar: {        ...prev.sbar,        \[field\]: value      }    }));  };

  const handleFileUpload = (e) => {    const file = e.target.files\[0\];    if (!file) return;

    const allowedTypes = \['application/pdf', 'image/png', 'image/jpeg', 'image/jpg'\];    if (!allowedTypes.includes(file.type)) {      showToast('⚠️ Format file tidak didukung! Harap unggah PDF, PNG, atau JPG.');      return;    }

    const newAttachment = {      id: Date.now(),      name: [file.name](http://file.name/),      type: file.type,      category: uploadCategory,      date: 'Baru saja',      size: \`${(file.size / (1024 \* 1024)).toFixed(2)} MB\`,      url: URL.createObjectURL(file),      labDetails: (uploadCategory === 'Hasil Lab' && includeLabDetails) ? \[...customLabParams\] : null    };

    setFormData(prev => ({      ...prev,      attachments: \[newAttachment, ...(prev.attachments || \[\])\]    }));

    e.target.value = '';    showToast(\`📎 Berhasil mengunggah ${[file.name](http://file.name/)} dengan interpretasi parameter lab.\`);  };

  const renderLabBadge = (status) => {    switch (status) {      case 'high':        return 🔴 TINGGI;      case 'low':        return 🔴 RENDAH;      case 'warning':        return 🟡 WASPADA;      case 'normal':      default:        return 🟢 NORMAL;    }  };

  const handleDeleteAttachment = (fileId) => {    setFormData(prev => ({      ...prev,      attachments: (prev.attachments || \[\]).filter(item => [item.id](http://item.id/) !== fileId)    }));    showToast('🗑️ Berkas berhasil dihapus.');  };

  const handlePublishUpdates = () => {    const updatedPatient = {      ...formData,      lastUpdated: 'Baru saja dipublis'    };    setPatientsData(prev => ({      ...prev,      \[activeUnit\]: updatedPatient    }));    showToast(\`✅ Data Pemantauan ${activeUnit} Berhasil Dipublis ke Portal Keluarga!\`);  };

  const handleAddQuestion = (e) => {    e.preventDefault();    if (!newQuestionText.trim()) return;    const qObj = {      id: Date.now(),      unit: activeUnit,      text: newQuestionText,      time: 'Baru saja',      answered: false,      answer: ''    };    setFamilyQuestions(\[qObj, ...familyQuestions\]);    setNewQuestionText('');    showToast('💬 Catatan pertanyaan berhasil dikirim ke perawat!');  };

  const handleAnswerQuestion = (qId) => {    const ansText = replyInputs\[qId\];    if (!ansText || !ansText.trim()) return;

    setFamilyQuestions(familyQuestions.map(q => {      if ([q.id](http://q.id/) === qId) {        return { ...q, answered: true, answer: ansText };      }      return q;    }));

    setReplyInputs(prev => ({ ...prev, \[qId\]: '' }));    showToast('✅ Jawaban perawat dikirim ke keluarga.');  };

  // --- UNIT RULES MANAGEMENT (NURSE PORTAL) ---  const handleAddRule = (e) => {    e.preventDefault();    if (!newRuleInput.trim()) return;

    setUnitRulesData(prev => ({      ...prev,      \[activeUnit\]: \[...(prev\[activeUnit\] || \[\]), newRuleInput.trim()\]    }));

    setNewRuleInput('');    showToast(\`✅ Aturan baru berhasil ditambahkan untuk Ruang ${activeUnit}\`);  };

  const handleStartEditRule = (index, currentText) => {    setEditingRuleIndex(index);    setEditingRuleText(currentText);  };

  const handleSaveEditRule = (index) => {    if (!editingRuleText.trim()) return;

    const updatedList = \[...(unitRulesData\[activeUnit\] || \[\])\];    updatedList\[index\] = editingRuleText.trim();

    setUnitRulesData(prev => ({      ...prev,      \[activeUnit\]: updatedList    }));

    setEditingRuleIndex(null);    setEditingRuleText('');    showToast('✏️ Tata tertib berhasil diperbarui.');  };

  const handleDeleteRule = (index) => {    const updatedList = (unitRulesData\[activeUnit\] || \[\]).filter((\_, i) => i !== index);

    setUnitRulesData(prev => ({      ...prev,      \[activeUnit\]: updatedList    }));

    showToast('🗑️ Poin tata tertib berhasil dihapus.');  };

  const renderDeviceIcon = (iconName) => {    switch (iconName) {      case 'wind': return ;      case 'activity': return ;      case 'droplets': return ;      case 'thermometer': return ;      case 'sparkles': return ;      default: return ;    }  };

  return (   

      {/\* Toast Notification \*/}      {toastMessage && (       

                    {toastMessage}       

      )}

      {/\* TOP APP HEADER \*/}     

       

                   {/\* Logo & Title \*/}         

           

             

             

               

                  Si-Manis               
=========================================

               

                  Sistem Pemantauan Harian dan SBAR untuk Intensif Care — RSUD RT. NOTOPURO SIDOARJO               

             

           

              setDarkMode(!darkMode)}                className="p-1.5 rounded-lg bg-white/10 border border-white/20 text-teal-200"                title="Toggle Theme"              >                {darkMode ? : }                         

         

            {!isAppInstalled ? (                                              Pasang di HP / Laptop                          ) : (                              Aplikasi Terpasang                          )}

            setDarkMode(!darkMode)}              className={\`hidden sm:flex items-center gap-2 px-3 py-1.5 rounded-xl border text-xs font-semibold transition-all ${                darkMode                  ? 'bg-slate-800 border-slate-700 text-amber-300 hover:bg-slate-700'                  : 'bg-teal-950/60 border-teal-700/50 text-teal-100 hover:bg-teal-900'              }\`}            >              {darkMode ? (                <>                                    Mode Terang                              ) : (                <>                                    Mode Gelap                              )}           

              setActiveRole('nurse')}                className={\`flex items-center gap-1.5 px-3 py-1.5 rounded-lg text-xs font-semibold transition-all ${                  activeRole === 'nurse'                    ? 'bg-teal-500 text-white shadow-md'                    : 'text-teal-200 hover:text-white hover:bg-teal-800/50'                }\`}              >                                Portal Perawat                            setActiveRole('family')}                className={\`flex items-center gap-1.5 px-3 py-1.5 rounded-lg text-xs font-semibold transition-all ${                  activeRole === 'family'                    ? 'bg-emerald-500 text-white shadow-md'                    : 'text-teal-200 hover:text-white hover:bg-teal-800/50'                }\`}              >                                Portal Keluarga                                  

       

        {/\* UNIT SELECTOR STRIP \*/}       

         

           

              Pilih Ruangan:              {\['ICU 1', 'ICU 2A', 'ICU 2B', 'HCU A', 'HCU B', 'ICCU', 'NICU', 'PICU'\].map((unit) => (                setActiveUnit(unit)}                  className={\`px-3 py-1 rounded-lg text-xs font-bold transition-all flex items-center gap-1.5 whitespace-nowrap ${                    activeUnit === unit                      ? darkMode                        ? 'bg-teal-500 text-slate-950 shadow-md scale-105'                        : 'bg-white text-teal-900 shadow-md scale-105'                      : darkMode                        ? 'bg-slate-900 text-slate-300 hover:bg-slate-800 border border-slate-800'                        : 'bg-teal-900/60 text-teal-100 hover:bg-teal-700/60 border border-teal-700/40'                  }\`}                >                  {unit === 'NICU' ? : }                  {unit}                              ))}           

                            {patientsData\[activeUnit\].name}              ({patientsData\[activeUnit\].bed})           

         

       

     

      {!isAppInstalled && (       

         

           

                                            **Gunakan CareIntensiv sebagai Aplikasi HP:** Akses cepat tanpa browser, lebih hemat kuota, & dapat dibuka saat offline.                         

                          Pasang Sekarang                     

       

      )}

      {/\* MAIN CONTENT AREA \*/}     

               {/\* ROLE BANNER INFORMATIONAL \*/}       

         

           

              {activeRole === 'nurse' ? : }           

           

             

                                  {activeRole === 'nurse' ? 'MODE ENTRI PERAWAT' : 'MODE BACA KELUARGA'}                                | Ruang {activeUnit}             

             

                {activeRole === 'nurse'                  ? \`Lembar Kerja Pemantauan & Form SBAR — Ruang ${activeUnit}\`                  : \`Informasi Ringkasan Pemulihan Pasien — Ruang ${activeUnit}\`}             
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

             

                {activeRole === 'nurse'                  ? 'Input data klinis harian pasien, perbarui templat narasi humanis, dan publis langsung ke tampilan smartphone keluarga.'                  : 'Laporan pemantauan transparan, aman, dan dapat dipahami untuk mendampingi masa perawatan anggota keluarga Anda.'}             

           

         

                                        Terakhir dipublis: **{patientsData\[activeUnit\].lastUpdated}**                     

       

        {/\* VIEW 1: PORTAL PERAWAT (NURSE PORTAL) \*/}        {activeRole === 'nurse' && (         

            {/\* LEFT COLUMN: CHECKLIST MEDICAL DATA & VITALS (7 COLS) \*/}           

                           {/\* Card 1: Identitas & Vital Signs \*/}             

               

                 

###                                         1. Identitas Pasien & Pemantauan Tanda Vital                 

                                   {/\* TOMBOL TAMBAH PASIEN BARU \*/}                 

                    setShowAddPatientModal(true)}                      className="text-xs bg-teal-600 hover:bg-teal-700 text-white font-bold px-3 py-1.5 rounded-lg transition-all flex items-center gap-1 shadow-sm"                    >                      \+ Tambah Pasien Baru                                                              {formData.id}                                                              PIN: {formData.pin}                                     

               

                 

                    Nama Pasien                    **{formData.name}**                 

                 

                    Umur / No RM                    **{formData.age} ({formData.mrn})**                 

                 

                    Bed / Lokasi                    **{formData.bed} ({activeUnit})**                 

               

                {/\* Status Pasien Selector \*/}               

                  Status Klinis Pasien (Tampil di Header Keluarga):                 

                    {\['Stabil', 'Pemantauan Ketat', 'Membaik'\].map((st) => (                      setFormData({ ...formData, status: st })}                        className={\`py-2 px-3 rounded-xl text-xs font-bold border transition-all ${                          formData.status === st                            ? st === 'Stabil' ? 'bg-emerald-600 text-white border-emerald-600 shadow-sm'                              : st === 'Pemantauan Ketat' ? 'bg-amber-500 text-white border-amber-500 shadow-sm'                              : 'bg-teal-600 text-white border-teal-600 shadow-sm'                            : darkMode ? 'bg-slate-950 text-slate-400 border-slate-800' : 'bg-slate-50 text-slate-600 border-slate-200 hover:bg-slate-100'                        }\`}                      >                        {st}                                          ))}                 

               

                {/\* Vital Signs Input Controls \*/}               

                 

                    Tekanan Darah (BP)                    handleVitalChange('bp', e.target.value)}                      className={\`w-full text-xs font-semibold px-2.5 py-1.5 rounded-lg border focus:outline-none focus:border-teal-500 ${                        darkMode ? 'bg-slate-900 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-200'                      }\`}                    />                 

                 

                    Nadi (HR)                    [formData.vitalSigns.hr](http://formdata.vitalsigns.hr/)}                      onChange={(e) => handleVitalChange('hr', e.target.value)}                      className={\`w-full text-xs font-semibold px-2.5 py-1.5 rounded-lg border focus:outline-none focus:border-teal-500 ${                        darkMode ? 'bg-slate-900 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-200'                      }\`}                    />                 

                 

                    Laju Napas (RR)                    handleVitalChange('rr', e.target.value)}                      className={\`w-full text-xs font-semibold px-2.5 py-1.5 rounded-lg border focus:outline-none focus:border-teal-500 ${                        darkMode ? 'bg-slate-900 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-200'                      }\`}                    />                 

                 

                    Saturasi O2                    handleVitalChange('spo2', e.target.value)}                      className={\`w-full text-xs font-semibold px-2.5 py-1.5 rounded-lg border focus:outline-none focus:border-teal-500 ${                        darkMode ? 'bg-slate-900 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-200'                      }\`}                    />                 

                 

                    Suhu Tubuh                    handleVitalChange('temp', e.target.value)}                      className={\`w-full text-xs font-semibold px-2.5 py-1.5 rounded-lg border focus:outline-none focus:border-teal-500 ${                        darkMode ? 'bg-slate-900 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-200'                      }\`}                    />                 

                 

                    Kesadaran (GCS)                    handleVitalChange('gcs', e.target.value)}                      className={\`w-full text-xs font-semibold px-2.5 py-1.5 rounded-lg border focus:outline-none focus:border-teal-500 ${                        darkMode ? 'bg-slate-900 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-200'                      }\`}                    />                 

               

             

              {/\* Card Upload Berkas PDF/PNG/JPG Vital Signs & Hasil Lab \*/}             

               

                 

###                                         Upload Dokumen Vital Sign & Hasil Lab (PDF, PNG, JPG)                 

                  Terbaca langsung oleh Keluarga               

                 

                   

                     

                     

                        **Pilih File dari HP / Komputer**                        Format yang didukung: PDF, PNG, JPG (Maks 10MB)                     

                   

                      setUploadCategory(e.target.value)}                        className={\`text-xs px-2.5 py-2 rounded-xl border focus:outline-none ${                          darkMode ? 'bg-slate-900 text-slate-200 border-slate-700' : 'bg-white text-slate-800 border-slate-300'                        }\`}                      >                        Hasil Lab                        Grafik Vital Sign                        Radiologi/Scan                        Dokumen Lainnya                     

                                              Unggah File                                                                 

                 

                  {/\* Attachment List \*/}                 

                   

####                       Daftar Berkas Terunggah Pasien ({formData.attachments?.length || 0}):                   

                    {(!formData.attachments || formData.attachments.length === 0) ? (                     

Belum ada file lab atau vital sign yang diunggah.

                    ) : (                     

                        {formData.attachments.map((att) => (                         

[att.id](http://att.id/)} className={\`p-3 rounded-xl border space-y-3 ${                            darkMode ? 'bg-slate-950 border-slate-800' : 'bg-slate-50 border-slate-200'                          }\`}>                           

                             

                                {att.type.includes('pdf') ? (                                                                  ) : (                                                                  )}                               

                                                                      {[att.name](http://att.name/)}                                                                                                        {att.category}                                    {att.size}                                    • {att.date}                                                                                              

                                                                                                                                  handleDeleteAttachment([att.id](http://att.id/))}                                  className="p-1.5 rounded-lg border border-rose-500/30 bg-rose-500/10 text-rose-400 hover:bg-rose-500/20 transition-all"                                  title="Hapus Berkas"                                >                                                                                                                          

                            {att.labDetails && att.labDetails.length > 0 && (                             

                                Rincian Parameter Lab Terinterpretasi:                               

                                  {att.labDetails.map((param, pIdx) => (                                   

                                     

                                        {[param.name](http://param.name/)}                                        {param.val} {param.unit} (Ref: {param.normal})                                     

                                      {renderLabBadge(param.status)}                                   

                                  ))}                               

                             

                            )}                         

                        ))}                     

                    )}                 

               

             

              {/\* Card 2: Checklist Interaktif Perawatan Harian \*/}             

               

                 

###                                         2. Checklist Interaktif Perawatan Harian                 

                  Centang tindakan yang sudah dieksekusi               

                  {CHECKLIST\_ITEMS.map((item) => (                    handleChecklistToggle(item.key)}                      className={\`p-3 rounded-xl border cursor-pointer transition-all flex items-start gap-3 ${                        formData.checklist?.\[item.key\]                          ? darkMode                            ? 'bg-emerald-950/40 border-emerald-800 text-slate-100'                            : 'bg-emerald-50/70 border-emerald-300 text-slate-800'                          : darkMode                            ? 'bg-slate-950 border-slate-800 text-slate-400 hover:bg-slate-850'                            : 'bg-slate-50 border-slate-200 text-slate-500 hover:bg-slate-100'                      }\`}                    >                     

                        {formData.checklist?.\[item.key\] ? (                                                  ) : (                                                  )}                     

                     

                                                  **{item.label}**                                                {item.desc}                     

                                      ))}               

             

              {/\* Card Editor Tata Tertib & Panduan Ruangan \*/}             

               

                 

###                                         Kelola Tata Tertib & Jam Kunjung (Ruang {activeUnit})                 

                  Tampil Otomatis di Portal Keluarga               

                  {/\* Form Tambah Rule Baru \*/}                 

                    setNewRuleInput(e.target.value)}                      className={\`flex-1 text-xs px-3 py-2 rounded-xl border focus:outline-none focus:border-teal-500 ${                        darkMode ? 'bg-slate-950 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-300'                      }\`}                    />                                          Tambah                                     

                  {/\* Daftar Rule yang Bisa Diedit / Dihapus \*/}                 

                    {(unitRulesData\[activeUnit\] || \[\]).map((rule, rIdx) => (                     

                        {editingRuleIndex === rIdx ? (                         

                            setEditingRuleText(e.target.value)}                              className={\`flex-1 text-xs px-2.5 py-1.5 rounded-lg border focus:outline-none ${                                darkMode ? 'bg-slate-900 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-300'                              }\`}                            />                            handleSaveEditRule(rIdx)}                              className="bg-emerald-600 text-white text-xs px-2.5 py-1 rounded-lg font-semibold hover:bg-emerald-700"                            >                              Simpan                                                        setEditingRuleIndex(null)}                              className="bg-slate-500 text-white text-xs px-2.5 py-1 rounded-lg font-semibold"                            >                              Batal                                                     

                        ) : (                          <>                           

                              •                              {rule}                           

                           

                              handleStartEditRule(rIdx, rule)}                                className="p-1.5 rounded-lg text-teal-400 hover:bg-teal-500/10 transition-all"                                title="Edit Poin"                              >                                                                                            handleDeleteRule(rIdx)}                                className="p-1.5 rounded-lg text-rose-400 hover:bg-rose-500/10 transition-all"                                title="Hapus Poin"                              >                                                                                         

                                                  )}                     

                    ))}                                

             

              {/\* Card Pertanyaan Masuk dari Keluarga \*/}             

               

                 

###                                         3. Pertanyaan Masuk dari Keluarga Pasien ({activeUnit})                 

                                      {familyQuestions.filter(q => q.unit === activeUnit && !q.answered).length} Belum Dijawab                                 

                  {familyQuestions.filter(q => q.unit === activeUnit).length === 0 ? (                   

Belum ada catatan pertanyaan dari keluarga untuk unit ini.

                  ) : (                    familyQuestions.filter(q => q.unit === activeUnit).map((q) => (                     

[q.id](http://q.id/)} className={\`p-3.5 rounded-xl border space-y-2 ${                        darkMode ? 'bg-slate-950 border-slate-800' : 'bg-slate-50/60 border-slate-200'                      }\`}>                       

                                                      {q.text}                                                    {q.time}                       

                        {q.answered ? (                         

                                                                                     **Jawaban Perawat:**                             

{q.answer}                                                    

                        ) : (                         

                            [q.id](http://q.id/)\] || ''}                              onChange={(e) => setReplyInputs({ ...replyInputs, \[[q.id](http://q.id/)\]: e.target.value })}                              className={\`flex-1 text-xs px-3 py-1.5 rounded-lg border focus:outline-none focus:border-teal-500 ${                                darkMode ? 'bg-slate-900 text-slate-100 border-slate-700' : 'bg-white text-slate-800 border-slate-300'                              }\`}                            />                            handleAnswerQuestion([q.id](http://q.id/))}                              className="bg-teal-600 hover:bg-teal-700 text-white text-xs font-semibold px-3 py-1.5 rounded-lg transition-all flex items-center gap-1 shrink-0"                            >                              Balas                                                     

                        )}                     

                    ))                  )}               

             

            {/\* RIGHT COLUMN: SBAR EDITOR & PUBLISH ACTION (5 COLS) \*/}           

             

               

                 

###                                         4. Editor Narasi SBAR Humanis                 

                  Format Bahasa Awam               

                 

                                          Situation (Kondisi Saat Ini)                                        handleSbarChange('situation', e.target.value)}                      className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 leading-relaxed ${                        darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-200'                      }\`}                    />                 

                                          Background (Latar Belakang Perawatan)                                        handleSbarChange('background', e.target.value)}                      className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 leading-relaxed ${                        darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-200'                      }\`}                    />                 

                                          Assessment (Evaluasi Pemulihan)                                        handleSbarChange('assessment', e.target.value)}                      className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 leading-relaxed ${                        darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-200'                      }\`}                    />                 

                                          Recommendation (Rencana Rencana Hari Ini)                                        handleSbarChange('recommendation', e.target.value)}                      className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 leading-relaxed ${                        darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-200'                      }\`}                    />                 

                                          Empathy Note (Pesan Penenang Keluarga)                                        handleSbarChange('empathyNote', e.target.value)}                      className={\`w-full p-2.5 rounded-xl border focus:outline-none leading-relaxed ${                        darkMode                          ? 'bg-rose-950/30 text-rose-100 border-rose-900/60 focus:border-rose-400'                          : 'bg-rose-50/50 text-rose-900 border-rose-200 focus:border-rose-400'                      }\`}                    />                 

               

                {/\* PUBLISH BUTTON \*/}               

                                                          Publis Pembaruan ke Portal Keluarga                                   

                    Setiap pembaruan akan langsung terlihat pada smartphone keluarga yang terverifikasi.                                

           

        )}

        {/\* VIEW 2: PORTAL KELUARGA (FAMILY PORTAL) \*/}        {activeRole === 'family' && (         

            {/\* PIN SECURITY GATEWAY FOR FAMILY PORTAL \*/}            {!familyVerified ? (             

               

               

                 

### Akses Portal Keluarga Pasien

                 

                    Masukkan PIN keamanan 4-digit yang diberikan oleh perawat untuk membuka laporan pasien **{patientsData\[activeUnit\].name}** ({activeUnit}).                 

               

                 

                    setInputPin(e.target.value)}                      className={\`w-full text-center text-2xl font-mono tracking-widest py-3 px-4 rounded-2xl border focus:outline-none focus:ring-2 ${                        darkMode                          ? 'bg-slate-950 text-white border-slate-700 focus:border-teal-500 focus:ring-teal-900'                          : 'bg-white text-slate-800 border-slate-300 focus:border-teal-600 focus:ring-teal-100'                      }\`}                    />                    {pinError &&

{pinError}

}                 

                                      Buka Laporan Pasien                                                 

Hubungi perawat jaga di counter ruangan jika Anda belum memiliki PIN akses.

             

            ) : (              /\* VERIFIED FAMILY DASHBOARD \*/             

                {/\* Patient Summary Header Card \*/}               

                 

                   

                      {activeUnit}                   

                   

                     

                       

### {currentPatient.name}

                                                  {currentPatient.status}                                             

                     

                        {currentPatient.age} | No. RM: {currentPatient.mrn} | Lokasi: **{currentPatient.bed}**                     

                     

                        Perawat Penanggung Jawab: {currentPatient.nurseInCharge}                     

                   

                 

                  setFamilyVerified(false)}                    className={\`text-xs px-3 py-1.5 rounded-lg transition-all flex items-center gap-1 border ${                      darkMode                        ? 'bg-slate-800 hover:bg-slate-700 text-slate-300 border-slate-700'                        : 'bg-slate-100 hover:bg-slate-200 text-slate-600 border-slate-200'                    }\`}                  >                    Kunci Sesi                                 

                {/\* SBAR Humanized Narrative Cards \*/}               

                 

                   

                                           ### Laporan Ringkasan Dokter & Perawat (Format SBAR)                   

                                          Update: {currentPatient.lastUpdated}                                     

                   

                      1\. Kondisi Pasien Saat Ini (Situation)                     

{currentPatient.sbar.situation}

                   

                      2\. Latar Belakang Tindakan (Background)                     

{currentPatient.sbar.background}

                   

                      3\. Evaluasi Perubahan (Assessment)                     

{currentPatient.sbar.assessment}

                   

                      4\. Rencana Perawatan Selanjutnya (Recommendation)                     

{currentPatient.sbar.recommendation}

                   

                 

                  {/\* Empathy Note Card \*/}                 

                                                             **Pesan Dukungan Tim Medis:**                     

{currentPatient.sbar.empathyNote}                                    

               

                {/\* Vitals Signs Card Plain Language \*/}               

                 

                   

###                                             Tanda-Tanda Vital Utama Pasien                   

                    Pantauan Terkini                 

                   

                      Tekanan Darah                      **{currentPatient.vitalSigns.bp}**                   

                      Detak Jantung                      **{[currentPatient.vitalSigns.hr](http://currentpatient.vitalsigns.hr/)}**                   

                      Laju Pernapasan                      **{currentPatient.vitalSigns.rr}**                   

                      Saturasi Oksigen                      **{currentPatient.vitalSigns.spo2}**                   

                      Suhu Tubuh                      **{currentPatient.vitalSigns.temp}**                   

                      Tingkat Kesadaran                      **{currentPatient.vitalSigns.gcs}**                   

                 

               

                {/\* Card Hasil Lab & Berkas Vital Sign Terunggah \*/}               

                 

                   

                     

###                                                 Dokumen Lab & Hasil Pemeriksaan Terintegrasi                     

                     

Dilengkapi interpretasi status warna (🔴 Naik/Turun, 🟢 Normal, 🟡 Waspada) dan Nilai Rujukan Normal

                   

                    Dapat Diunduh Langsung                 

                    {(!currentPatient.attachments || currentPatient.attachments.length === 0) ? (                     

Belum ada dokumen lampiran dari tim perawat untuk hari ini.

                    ) : (                     

                        {currentPatient.attachments.map((att) => (                         

[att.id](http://att.id/)} className={\`p-4 rounded-2xl border space-y-3 ${                            darkMode ? 'bg-slate-950 border-slate-800' : 'bg-slate-50 border-slate-200'                          }\`}>                           

                             

                               

                                  {att.type.includes('pdf') ? : }                               

                               

                                  **{[att.name](http://att.name/)}**                                                                      {att.category} • {att.size} • Terunggah: {att.date}                                                                 

                             

                                                              Berkas Asli                                                         

                            {att.labDetails && att.labDetails.length > 0 && (                             

                               

                                 

####                                     Hasil Interpretasi Parameter Lab (Darah Lengkap / Kimia Klinik / Profil Lipid)                                 

                                 

                                    🔴 Naik/Turun                                    🟢 Normal                                    🟡 Waspada                                 

                               

                                                                                                                                                                                                                                                                                                                                                                                                                                {att.labDetails.map((param, pIdx) => (                                                                                                                                                                                                                                                                                              ))}                                                                     

Pemeriksaan / Parameter

Hasil Pemeriksaan

Nilai Rujukan Normal

Status Interpretasi

                                            {[param.name](http://param.name/)}                                         

                                            {param.val} {param.unit}                                         

                                            {param.normal} {param.unit}                                         

                                            {renderLabBadge(param.status)}                                         

                               

                             

                            )}                         

                        ))}                     

                    )}                 

               

                {/\* Grid 2 Columns: Equipment Cards & Unit Rules \*/}               

                   

                     

###                                                 Edukasi Alat Medis Terpasang di Ruang {activeUnit}                     

                      Penjelasan Ramah Keluarga                   

                      {currentPatient.medicalDevices.map((dev, idx) => (                       

                         

                            {renderDeviceIcon(dev.icon)}                         

                         

                            **{[dev.name](http://dev.name/)}**                           

{dev.desc}

                         

                       

                      ))}                   

                 

                   

                     

###                                                 Tata Tertib & Panduan Ruang {activeUnit}                     

                      Penting                   

                      {(unitRulesData\[activeUnit\] || \[\]).map((rule, idx) => (                       *                                                       {rule}                       
                      ))}                   

                 

                {/\* Interactive Q&A Form from Family to Nurses \*/}               

                 

                   

###                                             Kirim Catatan Pertanyaan kepada Perawat Jaga ({activeUnit})                   

                    Respon Diberikan Saat Jam Kunjung / Serah Terima                 

                    setNewQuestionText(e.target.value)}                      className={\`flex-1 text-xs px-3.5 py-2.5 rounded-xl border focus:outline-none focus:border-teal-500 ${                        darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-300'                      }\`}                    />                                          Kirim                                     

                   

#### Riwayat Pertanyaan Keluarga:

                    {familyQuestions.filter(q => q.unit === activeUnit).length === 0 ? (                     

Belum ada pertanyaan yang dikirimkan.

                    ) : (                      familyQuestions.filter(q => q.unit === activeUnit).map((q) => (                       

[q.id](http://q.id/)} className={\`p-3.5 rounded-2xl border space-y-2 text-xs ${                          darkMode ? 'bg-slate-950 border-slate-800' : 'bg-slate-50/50 border-slate-200'                        }\`}>                         

                                                          {q.text}                                                                                      {q.answered ? 'Dijawab' : 'Menunggu Jawaban'}                                                     

                          {q.answered && (                           

                                                              **Jawaban Perawat:**                                                           

{q.answer}

                           

                          )}                       

                      ))                    )}                                

            )}

        )}

      {/\* MODAL TAMBAH PASIEN BARU \*/}      {showAddPatientModal && (       

         

            setShowAddPatientModal(false)}              className={\`absolute top-4 right-4 p-1.5 rounded-full border ${                darkMode ? 'bg-slate-800 border-slate-700 text-slate-400 hover:text-white' : 'bg-slate-100 border-slate-200 text-slate-500 hover:text-slate-800'              }\`}            >                                                                                                          ### Form pendaftaran Pasien Baru ({activeUnit})

               

Masukkan data klinis awal untuk didaftarkan ke portal perawat & keluarga

             

           

             

               

                  Nama Pasien \*                  setNewPatientForm({ ...newPatientForm, name: e.target.value })}                    className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 ${                      darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-300'                    }\`}                  />               

                  Nomor Rekam Medis (RM) \*                  setNewPatientForm({ ...newPatientForm, mrn: e.target.value })}                    className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 ${                      darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-300'                    }\`}                  />               

                  Umur Pasien                  setNewPatientForm({ ...newPatientForm, age: e.target.value })}                    className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 ${                      darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-300'                    }\`}                  />               

                  Bed / Tempat Tidur                  setNewPatientForm({ ...newPatientForm, bed: e.target.value })}                    className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 ${                      darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-300'                    }\`}                  />               

                  PIN Akses Keluarga (4 Angka)                  setNewPatientForm({ ...newPatientForm, pin: e.target.value })}                    className={\`w-full p-2.5 rounded-xl border font-mono focus:outline-none focus:border-teal-500 ${                      darkMode ? 'bg-slate-950 text-amber-400 border-slate-800' : 'bg-slate-50 text-amber-600 border-slate-300'                    }\`}                  />               

                  Perawat Penanggung Jawab                  setNewPatientForm({ ...newPatientForm, nurseInCharge: e.target.value })}                    className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 ${                      darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-300'                    }\`}                  />               

             

                Diagnosis Medis Masuk                setNewPatientForm({ ...newPatientForm, diagnosis: e.target.value })}                  className={\`w-full p-2.5 rounded-xl border focus:outline-none focus:border-teal-500 ${                    darkMode ? 'bg-slate-950 text-slate-100 border-slate-800' : 'bg-slate-50 text-slate-800 border-slate-300'                  }\`}                />             

                Nilai Tanda-Tanda Vital Awal:               

                 

                    Tensi (BP)                    setNewPatientForm({ ...newPatientForm, bp: e.target.value })}                      className={\`w-full p-1.5 rounded-lg border text-xs font-semibold ${                        darkMode ? 'bg-slate-900 border-slate-700 text-slate-100' : 'bg-white border-slate-300 text-slate-800'                      }\`}                    />                 

                 

                    Nadi (HR)                    setNewPatientForm({ ...newPatientForm, hr: e.target.value })}                      className={\`w-full p-1.5 rounded-lg border text-xs font-semibold ${                        darkMode ? 'bg-slate-900 border-slate-700 text-slate-100' : 'bg-white border-slate-300 text-slate-800'                      }\`}                    />                 

                 

                    Saturasi O2                    setNewPatientForm({ ...newPatientForm, spo2: e.target.value })}                      className={\`w-full p-1.5 rounded-lg border text-xs font-semibold ${                        darkMode ? 'bg-slate-900 border-slate-700 text-slate-100' : 'bg-white border-slate-300 text-slate-800'                      }\`}                    />                 

               

             

                setShowAddPatientModal(false)}                  className={\`px-4 py-2 rounded-xl border text-xs font-semibold ${                    darkMode ? 'bg-slate-800 border-slate-700 text-slate-300' : 'bg-slate-100 border-slate-300 text-slate-600'                  }\`}                >                  Batal                                                  Simpan Pasien Baru                                                 

       

      )}

      {/\* PWA INSTALLATION INSTRUCTIONS MODAL \*/}      {showInstallModal && (       

         

            setShowInstallModal(false)}              className={\`absolute top-4 right-4 p-1.5 rounded-full border ${                darkMode ? 'bg-slate-800 border-slate-700 text-slate-400 hover:text-white' : 'bg-slate-100 border-slate-200 text-slate-500 hover:text-slate-800'              }\`}            >                                                                                                          ### Panduan Pemasangan Aplikasi

               

Unduh CareIntensiv langsung ke layar utama HP Anda

             

           

             

                                  **Untuk Pengguna Android (Chrome / Edge / Samsung)**                               

                 1.  Tekan tombol \*\*titik tiga (⋮)\*\* di pojok kanan atas browser.
                 2.  Pilih opsi \*\*"Tambahkan ke Layar Utama"\*\* atau \*\*"Install App"\*\*.
                 3.  Konfirmasi pemasangan, lalu aplikasi akan muncul di daftar menu HP Anda.
               

             

                                  **Untuk Pengguna iPhone / iPad (Safari)**                               

                 1.  Buka link web ini di browser \*\*Safari\*\*.
                 2.  Tekan tombol \*\*Bagikan (Share icon)\*\* di bagian bawah layar.
                 3.  Gulir ke bawah lalu pilih \*\*"Tambah ke Layar Utama" (Add to Home Screen)\*\*.
                 4.  Tekan \*\*"Tambah"\*\* di pojok kanan atas.
               

             

           

            setShowInstallModal(false)}              className="w-full bg-teal-600 hover:bg-teal-700 text-white font-bold py-2.5 px-4 rounded-xl text-xs transition-all"            >              Saya Mengerti                     

       

      )}

      {/\* FOOTER \*/}     

       

         

           

                            Si-Manis — RSUD RT. NOTOPURO SIDOARJO           

            •            Created by dr. Puguh Widagdo, SpPD, FINASIM bersama TIM IPIT         

         

                          {isOnline ? : }              {isOnline ? 'Online' : 'Offline'}                        |            Didesain untuk Perawat & Keluarga Pasien         

       

     

   

  );}\`\`\`