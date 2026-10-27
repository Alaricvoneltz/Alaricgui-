# ⚡ Alaric UI Library
Alaric UI Library adalah framework antarmuka (GUI) modern untuk Roblox yang sangat ringan, beranimasi mulus, dan mendukung sistem *Sub-Tab* yang dapat di-scroll (mirip Rayfield).

## 🚀 Cara Menggunakan (How to Load)
Pertama, muat (load) library dari link raw GitHub Anda:
```lua
local AlaricLibrary = loadstring(game:HttpGet("MASUKKAN_LINK_RAW_GITHUB_ANDA_DISINI"))()

1. Membuat Jendela (Window)
Membuat GUI Utama yang berisi judul dan sub-judul.
local Window = AlaricLibrary:CreateWindow({
    Name = "Alaric Hub",     -- Judul Utama Hub
    SubTitle = "By Risky"    -- Sub Judul
})

2. Membuat Tab & Sub-Tab
Library ini menggunakan sistem Tab (di sebelah kiri) dan Sub-Tab (di atas/header).
-- Membuat Tab Utama di kiri
local TabMain = Window:CreateTab({ Name = "Main Features" })

-- Membuat Sub-Tab di atas (Header)
local SubFarming = TabMain:CreateSubTab({ Name = "Farming Area" })
local SubSettings = TabMain:CreateSubTab({ Name = "Settings" })

3. Menambahkan Fitur (Toggles, Inputs, Dropdowns)
Tambahkan elemen ke dalam Sub-Tab yang sudah Anda buat sebelumnya.

--Membuat Toggle (Saklar)
SubFarming:CreateToggle({
    Name = "Auto Farm Rocks",
    Callback = function(Value)
        -- Kode ini berjalan setiap kali tombol ditekan
        if Value then
            task.spawn(function()
                -- Window.IsAlive memastikan loop berhenti jika tombol (X) ditekan!
                while Value and Window.IsAlive do 
                    print("Sedang farming...")
                    task.wait(1)
                end
            end)
        end
    end
})

--Membuat Input Angka
--(Otomatis memblokir input huruf/simbol, hanya angka yang diperbolehkan!)
SubSettings:CreateInput({
    Name = "WalkSpeed",
    Placeholder = "Ketik Angka...",
    Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
    end
})

--Membuat Dropdown (Pilihan)
SubSettings:CreateDropdown({
    Name = "Pilih Lokasi Teleport",
    Options = {"Spawn", "VIP Room", "Mining Area"},
    Callback = function(Option)
        print("Pemain memilih lokasi:", Option)
    end
})

4. Membuat Sistem Logger (Console Bawaan UI)
Anda bisa membuat tab khusus log untuk melihat progress script Anda dari dalam game tanpa menekan F9.
-- Buat Tab dan Sub-Tab khusus (Nama SubTab HARUS "System Logs")
local TabLogs = Window:CreateTab({ Name = "Logs Console" })
local SubLogs = TabLogs:CreateSubTab({ Name = "System Logs" })

-- Cara memunculkan pesan di logger:
Window:Log("Script berhasil dimuat!")
Window:Log("Memulai proses Auto-Farm...")

 PERINGATAN PENTING: Penggunaan Window.IsAlive
Di UI ini terdapat tombol Destroy (X) berwarna merah. Jika pengguna menekannya, GUI akan terhapus sepenuhnya.
Agar auto-farm/looping Anda tidak terus berjalan di background, Anda WAJIB menambahkan Window.IsAlive di setiap while loop Anda.
✅ Benar: while Value and Window.IsAlive do
❌ Salah: while Value do

