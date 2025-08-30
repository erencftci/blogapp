BlogApp

BlogApp, Node.js ve Express kullanılarak geliştirilmiş, EJS şablon motoru ile dinamik arayüz sağlayan, MySQL ve Sequelize ORM tabanlı bir blog uygulamasıdır. Rol tabanlı yetkilendirme (admin, moderator), kullanıcı kayıt/giriş işlemleri, blog ve kategori yönetimi, görsel yükleme, CSRF koruması ve e-posta ile parola sıfırlama gibi özellikler sunar.

Kullanılan Teknolojiler

Sunucu: Node.js, Express

Arayüz: EJS (template engine), Bootstrap 5

Veritabanı: MySQL, Sequelize ORM

Oturum & Yetkilendirme: express-session, connect-session-sequelize, cookie-parser, bcrypt

Güvenlik: csurf (CSRF koruması)

Dosya Yükleme: multer (görseller: public/images)

E-posta: nodemailer (SMTP)

Diğer: slugify (SEO uyumlu URL), path, fs

Klasör Yapısı

index.js: Uygulama girişi, middleware/route tanımları, model ilişkileri, sunucu başlatma

controllers/: İş mantığı (admin, auth, user)

routes/: HTTP rotaları (/admin, /account, genel kullanıcı rotaları)

models/: Sequelize modelleri (blog, category, user, role)

middlewares/: csrf, is-admin, is-moderator, locals, hata & log

helpers/: image-upload (multer), send-mail (nodemailer), slugfield (slugify)

views/: EJS sayfaları (kullanıcı, admin, auth, partials)

data/: db.js (Sequelize bağlantısı), dummy-data.js (örnek veri)

Kurulum

Önkoşullar: Node.js 16+ ve MySQL 8+ sürümleri kurulmalıdır.

Bağımlılıkların kurulumu: npm install komutu ile tüm bağımlılıklar yüklenir.

Veritabanı ve yapılandırma: MySQL üzerinde blogdb isminde bir veritabanı oluşturun. Üretimde gizli bilgiler .env dosyasında saklanmalıdır:

DB_HOST, DB_USER, DB_PASSWORD, DB_NAME

SESSION_SECRET

EMAIL_USERNAME, EMAIL_PASSWORD, EMAIL_FROM

Şema ve örnek veri (isteğe bağlı): index.js dosyasında geçici olarak sequelize.sync({ force: true }); ve dummyData(); fonksiyonları açılarak ilk çalıştırmada tablolar ve örnek veriler oluşturulur. Sonrasında bu satırlar kapatılmalıdır.

Çalıştırma: npm start komutu ile uygulama başlatılır. Varsayılan olarak http://localhost:1000
 adresinde çalışır. Statik dosyalar /static (public) ve /libs (node_modules) klasörlerinden servis edilir.

Önemli Rotalar

Genel: /, /blogs, /blogs/category/:slug, /blogs/:slug

Kimlik: /account/register, /account/login, /account/reset-password, /account/new-password/:token, /account/logout

Admin: /admin/blogs, /admin/categories, /admin/roles, /admin/users (+ alt rotalar)

Güvenlik Notları

CSRF koruması aktiftir; formlarda token kullanılır.

Üretimde gizli bilgiler .env dosyasında tutulmalı ve git deposuna eklenmemelidir.

Parola sıfırlama e-postasındaki bağlantıdaki domain ve port bilgileri ortamınıza uygun olarak .env içinden ayarlanmalıdır (APP_BASE_URL gibi).

Lisans

ISC
