# AMONO — publish guide (Polish)

## Co jest w tej paczce

To jest gotowa, statyczna strona Amono. Nie ma npm, frameworka, płatnego API ani osobnego serwera.

- `index.html` — landing page.
- `privacy.html` — osobna Privacy Policy.
- `thank-you/index.html` — strona po prawidłowym zapisaniu się na waitlistę.
- `AMONO_MASTER_cutout.webm` — film z przezroczystym tłem (przeglądarki obsługujące WebM alpha).
- `AMONO_MASTER_fallback.mp4` — fallback dla przeglądarek bez WebM alpha.
- `amono-logo.png`, `hero-poster.png`, `beach-wallpaper.jpg` — grafiki.
- `netlify.toml` — wskazuje Netlify, że pliki strony są w katalogu głównym repozytorium.

## Ważne: formularz waitlisty

Formularz w `index.html` jest zwykłym statycznym formularzem HTML. Ma `name="waitlist"`, `method="POST"`, `data-netlify="true"`, wymagane pole email, wymagany checkbox zgody oraz honeypot. Po wysłaniu Netlify powinien zapisać zgłoszenie i przejść do `/thank-you/`.

**W panelu Netlify trzeba raz włączyć Forms → Enable form detection, a następnie wykonać nowy deploy.** Netlify rozpoznaje formularze na podstawie HTML podczas deployu, nie w czasie otwierania strony.

## Najprostszy workflow — GitHub + istniejący projekt Netlify

### A. Umieść pliki w GitHub

1. Rozpakuj ZIP.
2. Otwórz folder `AMONO_SITE`. W środku od razu musisz widzieć `index.html`, `privacy.html` i `netlify.toml`.
3. Wejdź na https://github.com/ i utwórz nowe repozytorium o nazwie `amono-landing-page`.
4. Wybierz `Private` (repozytorium prywatne). Nie dodawaj README, `.gitignore` ani licencji — pliki są już w paczce.
5. Utwórz repozytorium.
6. W repozytorium kliknij `Add file` → `Upload files`.
7. Otwórz folder `AMONO_SITE` na komputerze i przeciągnij **jego zawartość** do przeglądarki GitHub (nie sam folder nadrzędny i nie ZIP). W repozytorium `index.html` ma być widoczny na pierwszym poziomie, obok `privacy.html`.
8. Kliknij `Commit changes`.

### B. Podłącz repozytorium do istniejącej strony Netlify

1. Zaloguj się do https://app.netlify.com/ i otwórz istniejący projekt Amono.
2. Wejdź w `Project configuration` → `Developer settings` → `Continuous deployment` → `Repository`.
3. Wybierz `Link repository` (albo `Manage repository` → `Link to a different repository`, zależnie od tego, czy projekt ma już repozytorium).
4. Wybierz GitHub i zezwól aplikacji Netlify na dostęp do repozytorium `amono-landing-page`.
5. Wybierz gałąź `main`.
6. Ustaw `Build command` jako puste (bez polecenia).
7. Ustaw `Publish directory` na `.` (pojedyncza kropka — katalog główny repozytorium).
8. Zapisz i uruchom deploy.

Jeśli nie ma opcji połączenia repozytorium w istniejącym projekcie, nie twórz od razu drugiej strony. Najpierw sprawdź `Project configuration` → `Developer settings` → `Continuous deployment` → `Repository`. Dokumentacja Netlify opisuje też ponowne podłączenie GitHub App dla istniejącego projektu.

### C. Włącz formularze

1. W projekcie Netlify otwórz `Forms`.
2. Jeśli widzisz `Enable form detection`, kliknij raz.
3. Po włączeniu wykonaj nowy deploy z repozytorium: w GitHub otwórz `index.html`, kliknij edycję i zapisz drobną zmianę (najbezpieczniej zmień tylko znak spacji w komentarzu HTML), albo użyj `Trigger deploy` w Netlify.
4. Poczekaj na status `Published`.
5. Otwórz `Forms`. Powinien pojawić się formularz o nazwie `waitlist`.

### D. Opublikuj stronę publicznie

W nowych projektach Netlify widoczność może domyślnie być `Private`. Odwiedzający nie zobaczą witryny, dopóki jej nie opublikujesz.

1. `Project configuration` → `General` → `Visitor access` → `Project visibility`.
2. Wybierz `Public` i zapisz.
3. Otwórz publiczny adres Netlify w oknie incognito, bez zalogowania.

**Uwaga:** widoczność projektu Netlify i widoczność repozytorium GitHub to dwie różne rzeczy. Repozytorium kodu jest publiczne, a witryna Netlify musi dodatkowo mieć ustawienie `Public`, żeby każdy mógł ją otworzyć.

### E. Test waitlisty

1. Otwórz stronę w oknie incognito.
2. Przewiń do waitlisty.
3. Wpisz testowy adres email, zaznacz checkbox zgody i wyślij.
4. Powinieneś trafić na stronę `/thank-you/`.
5. W Netlify wejdź w `Forms` → `waitlist` → `Submissions` i sprawdź testowy wpis oraz pole `email_updates_consent`.
6. Sprawdź też `Spam`, jeśli zgłoszenia nie widać na liście głównej.
7. Usuń testowy wpis, jeśli nie chcesz go zachować.

### F. Powiadomienia na Gmail

W Netlify: `Forms` → `Submission notifications` → `Add notification` → `Email notification`. Wpisz `amono.calendar@gmail.com` i potwierdź ewentualny mail weryfikacyjny.

## Bezpłatność — co jest, a czego nie obiecujemy

- GitHub Free umożliwia bezpłatne prywatne repozytorium.
- Netlify Forms jest bezpłatny i nielimitowany w aktualnych planach kredytowych Netlify.
- Netlify Free ma jednak twardy limit 300 kredytów miesięcznie. Transfer danych, żądania i produkcyjne wdrożenia zużywają kredyty. Po osiągnięciu limitu projekty mogą zostać wstrzymane do nowego okresu. Plan Free nie nalicza automatycznej dopłaty; nie włączaj płatnego planu ani auto-recharge.
- Dlatego można uruchomić tę wersję za £0/$0 na Free, ale nie można uczciwie obiecać nieograniczonego ruchu ani 100% dostępności przy dowolnej popularności.

## Kontrola jakości przed udostępnieniem

Sprawdź stronę na:

- telefonie: szerokość około 360–430 px;
- tablecie pionowo: około 768 px;
- tablecie poziomo / małym laptopie: około 1024 px;
- laptopie: 1366 px;
- dużym ekranie: 1920 px.

Na każdym urządzeniu sprawdź: menu, przycisk Join the waitlist, sceny interaktywnego telefonu, FAQ, Privacy Policy, Contact, odtwarzanie filmu i brak poziomego przewijania. Na iPhonie Safari może użyć pliku MP4 fallback, ponieważ przezroczystość WebM nie jest obsługiwana identycznie we wszystkich przeglądarkach.

## Prywatność — przed zbieraniem prawdziwych adresów

Privacy Policy opisuje Netlify jako dostawcę hostingu i obsługi formularza. Przed zaproszeniem prawdziwych użytkowników należy z rodzicem/opiekunem potwierdzić, kto jest administratorem danych, czy treść polityki prawidłowo identyfikuje tę osobę i jaki okres przechowywania jest faktycznie stosowany. Nie zbieraj dodatkowych danych, których formularz nie potrzebuje.

## Gdy Forms nadal pokazuje „No forms available”

W tej paczce formularz jest w statycznym `index.html`, a nie tworzony przez JavaScript. Wtedy sprawdź po kolei:

1. Czy `Forms → Form detection` jest włączone.
2. Czy ostatni deploy został wykonany **po** włączeniu Form detection i ma status `Published`.
3. Czy w deployowanej zawartości głównego katalogu jest `index.html` (nie `AMONO_SITE/index.html` jako dodatkowy poziom).
4. Czy widoczność projektu jest `Public`.
5. Czy w `Deploys` faktycznie opublikowany deploy pochodzi z gałęzi `main` i repozytorium `amono-landing-page`.

Jeśli po tych krokach formularz nadal nie pojawia się w Forms, nie wysyłaj kolejnych losowych deployów — otwórz `Deploy details` i sprawdź log `Post processing` / `Forms` albo skontaktuj się z Netlify Support z informacją, że statyczny formularz `waitlist` z `data-netlify="true"` nie został wykryty.
