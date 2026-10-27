# guvenapps
Güven Apps resmi web sitesi ve uygulama gizlilik politikaları

## Her sürümde site güncellemesi

Güven Phone'un yeni bir sürümü Google Play'de bütün kullanıcılara açıldığında site güncellenir. Dahili ya da kapalı testteki sürümler siteye yazılmaz.

### Önce sürümü doğrula

Üretimdeki sürüm adını ve yayın tarihini Semih'e sorarak doğrula. Uygulama deposundaki `docs/OPEN_WORK.md` yayın kaydı paketin hangi commit'ten derlendiğini (VCS revision) yazar. Metni o commit'ten al; `main`'in ucu henüz yayımlanmamış işi içerebilir.

### Metin nereden alınır

Metin elle yazılmaz, uygulamanın kendi metninden alınır (`~/Developer/guven-phone`, yalnız okunur):

- Kartlar: `feature/settings/src/main/java/com/guven/phone/feature/settings/ui/ReleaseNotesScreen.kt` içindeki `releaseNoteEntries()` sırası, metinleri `feature/settings/src/main/res/values-tr/strings_release_notes.xml` ve `values-en/strings_release_notes.xml`.
- Kısa özet: `app/src/main/play/release-notes/tr-TR/production.txt` ve `en-US/production.txt`.

Uygulamadaki liste eski sürümlerden kalan kartları da gösterir. Sitedeki yeni sürüm bölümüne yalnız o sürümde yeni olan kartlar girer; `releaseNoteEntries()` başındaki yorum hangilerinin yeni olduğunu söyler.

### Hangi sayfalar güncellenir

Türkçe ve İngilizce sayfalar aynı yapıda tutulur.

- Yenilikler: `guven-phone/yenilikler/index.html` ve `en/guven-phone/whats-new/index.html`. Yeni sürüm bölümü en üste eklenir, önceki sürümler altta kalır.
- Ana sayfa: `index.html` ve `en/index.html` içindeki "Son gelişmeler" kartı (sürüm, tarih, kısa cümle).
- Güven Phone sayfası: `guven-phone/index.html` ve `en/guven-phone/index.html` içindeki "Yenilikler" bölümü; yeni özellik listede yoksa "Öne çıkan özellikler"e eklenir.
- Uygulamada bir ad ya da akış değiştiyse sitedeki anlatım da değişir. Örnek: 2.0.23'te Sorun bildir bölümünün adı Geri bildirim oluyor ve E-postayla gönder düğmesi alıcıyı ve konuyu kendisi dolduruyor. 2.0.23 üretime çıkınca ana sayfadaki "Uygulamanın içinden" anlatımı ve Güven Phone sayfasındaki kısa cümle yeniden yazılır.
- Gizlilik politikası yalnız uygulamanın veri davranışı değiştiyse güncellenir.

### Yardım sayfaları

`guven-phone/yardim/` ve `en/guven-phone/help/` elle düzenlenmez; uygulamadaki Yardım Rehberi'nden üretilir. Yeni sürüm üretime çıkınca betiği paketin derlendiği commit'le çalıştır:

```
python3 -I tools/build_help_pages.py <guven-phone-commit>
```

Betik konu sırasını `HelpScreen.kt` içindeki `HelpTopic` listesinden, metinleri `values-tr` ve `values-en` altındaki `strings_help.xml` dosyalarından alır ve kaldırılan bir konunun sayfasını siler. Yenilikler kartlarındaki "Nasıl kullanılır" bağlantıları, kartın `releaseNoteEntries()` içindeki `helpTopic` değerine göre elle eklenir.

### Yayından önce

Yerelde `python3 -m http.server` ile aç; bağlantıları, başlık sırasını, "Ana içeriğe geç" bağlantısını ve dil seçimini iki dilde dene. Semih değişen metinleri baştan sona dinler ve onaylar. `main`'e push canlı yayındır (GitHub Pages); onaysız push yapılmaz. Push sonrası yeni sayfaları canlı sitede aç.

Siteye kişisel veri girmez: testçi adı, cihaz ayrıntısı ya da açık iş kaydı yazılmaz. İç iş takibi uygulama deposunda kalır.
