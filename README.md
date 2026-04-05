
2. class Urun:
    def __init__(self, isim, fiyat, stok):
        self.isim = isim
        self.fiyat = fiyat
        self.stok = stok

class Sepet:
    def __init__(self):
        self.urunler = {}
    def urun_ekle(self, urun, adet):
        if urun.stok >= adet:
            if urun.isim in self.urunler:
                self.urunler[urun.isim]['adet'] += adet # Aynı ürün eklenirse miktar artırılır
            else:
                self.urunler[urun.isim] = {'urun': urun, 'adet': adet}
            urun.stok -= adet # Stoktan düşme
            print(f"{adet} adet {urun.isim} sepete eklendi.")
        else:
            print(f"Yetersiz stok! {urun.isim} için kalan stok: {urun.stok}")
    def urun_sil(self, urun):
        if urun.isim in self.urunler:
            adet = self.urunler[urun.isim]['adet']
            urun.stok += adet # Ürün silindiğinde stok geri eklenir
            del self.urunler[urun.isim]
            print(f"{urun.isim} sepetten silindi.")
        if not self.urunler: # Sepette ürün kalmazsa sözlük zaten temizlenmiş olur
            self.urunler.clear() 
    def toplam_tutar(self):
        tutar = sum(item['urun'].fiyat * item['adet'] for item in self.urunler.values())
        return tutar
