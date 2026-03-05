- date: 2026-03-05
  cat: UI / navbar
  误: Navbar pertama hanya pakai `<span>` teks biasa untuk logo, tab pakai pill button dengan emoji
  正: Logo harus pakai icon mark (SVG) + wordmark; nav links plain text tanpa background
  则: Selalu pakai icon mark untuk branding; tab nav = plain text links, bukan pill/button style

- date: 2026-03-05
  cat: UI / spacing
  误: Nav items terlalu rapat (gap-1 antar tab, elemen action terlalu dekat)
  正: Nav tabs gap-8+; action items gap-6; navbar height h-16; px-8
  则: Default spacing untuk navbar professional = lebih lega dari yang terasa "cukup"

- date: 2026-03-05
  cat: UI / color
  误: Stats cards pakai full gradient background (from-indigo-500), chart bars semua warna sama (bg-gray-500 fallback)
  正: Stats cards = white + thin left-border accent; chart bars = CHART_COLORS dengan inline hex per kategori
  则: Warna digunakan untuk informasi, bukan dekorasi; gradient penuh = unprofessional

- date: 2026-03-05
  cat: binding / debug
  误: Tidak mengecek bind-category-select HTML options saat debug "camera tidak bisa di-link"
  正: Root cause: opsi ADAS/DMS-Camera tidak ada di dropdown; logic JS juga hanya handle 3 kategori lama
  则: Saat bug binding, cek dulu: (1) apakah opsi ada di dropdown HTML, (2) apakah filter JS sudah cover kategori baru
