# Google-Colab-Connect

* Colab üzerinde çalışma yapılabilmesi için öncelikle _Google Drive ile Colab'ı_ bağlantısı yapılmalıdır.
* Bunun için aşağıdaki kodları alıp Colab ortamında çalıştırabilirsiniz.


```
!apt-get install -y -qq software-properties-common python-software-properties module-init-tools
!add-apt-repository -y ppa:alessandro-strada/ppa 2>&1 > /dev/null
!apt-get update -qq 2>&1 > /dev/null
!apt-get -y install -qq google-drive-ocamlfuse fuse
from google.colab import auth
auth.authenticate_user()
from oauth2client.client import GoogleCredentials
creds = GoogleCredentials.get_application_default()
import getpass
!google-drive-ocamlfuse -headless -id={creds.client_id} -secret={creds.client_secret} < /dev/null 2>&1 | grep URL
vcode = getpass.getpass()
!echo {vcode} | google-drive-ocamlfuse -headless -id={creds.client_id} -secret={creds.client_secret}
```

* Kodu çalıştırınca karşınıza sırasıyla **2 adımlı kimlik doğrulama linkleri** gelecektir.
* Bu linklerdeki şifreleri kopyalayıp yapıştırdıktan sonra Enter'lamak bağlantının kurulması için yeterlidir.
