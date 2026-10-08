# KIYAAAA di Vercel (harga dimuat otomatis dari server)

Dashboard memanggil `/api/chart` (fungsi server Vercel) yang mengambil data Yahoo Finance
dari sisi server, tanpa proxy gratis. Hasil disimpan di cache Vercel 15 menit, jadi buka
berikutnya cepat dan Yahoo jarang dipanggil. Tidak perlu token atau environment variable.

Isi: `index.html` (menu), `breakout.html`, `rsi.html`, `rsi-sr.html`, `rsi-sr-time.html`, `api/chart.js`, `vercel.json`

- `rsi.html`: RSI(14) cross level 50 + CAGR.
- `rsi-sr.html`: RSI(14) + konfirmasi Support/Resistance (BUY: RSI naik dari Oversold di zona Support; SELL: RSI turun dari Overbought di zona Resistance atau breakdown Support). Memakai data OHLC dari `/api/chart` (tanpa `lite=1`).
- `rsi-sr-time.html`: sama seperti `rsi-sr.html` ditambah **Time Stop**: posisi yang sudah ditahan N bar dan belum untung dilepas di open bar berikutnya (opsi "Selalu" melepas di bar ke-N tanpa syarat).

## Pasang lewat GitHub tanpa upload folder
1. Ekstrak zip ini, lalu di repo GitHub pilih **Add file > Upload files** dan seret semua file
   hasil ekstrak (index.html, breakout.html, rsi.html, rsi-sr.html, rsi-sr-time.html, vercel.json) lalu **Commit changes**.
2. Fungsi server dibuat terpisah (cukup sekali, lewati kalau `api/chart.js` sudah ada di repo):
   **Add file > Create new file**, ketik nama `api/chart.js` (tanda `/` otomatis membuat folder `api`),
   tempel seluruh isi file `api_chart_js.txt`, lalu **Commit changes**.
3. Di vercel.com: **Add New > Project** > pilih repository > **Deploy**. Tunggu status **Ready**.
4. Tes fungsi server: buka `https://NAMA-PROYEK.vercel.app/api/chart?s=BBCA`.
   Kalau muncul deretan angka (d, o, h, l, c, v), fungsi bekerja.

## Alternatif lewat komputer (tanpa GitHub)
Pasang Node.js, lalu di folder ini jalankan `npm i -g vercel`, kemudian `vercel`
(login lewat browser) dan `vercel --prod`. Token tidak perlu disalin manual.

## Catatan
- Yahoo kadang membatasi alamat server cloud. Dashboard otomatis mengulang, memakai proxy
  lama sebagai cadangan, dan mengisi simbol gagal dari cache. Cek kartu Status Data.
- Saat bursa buka, candle hari ini belum final. Sinyal strategi baru valid setelah bursa tutup.
- Tab yang terbuka memuat ulang harga tiap 30 menit.
- Untuk edukasi dan simulasi, bukan rekomendasi investasi.
