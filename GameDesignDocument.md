# DEAD ZONE SURVIVAL
## Tài liệu Thiết kế Game (GDD) — Phiên bản 1.0

---

# PHẦN I — TỔNG QUAN

## 1.1 Tóm tắt dự án

**Tên game:** DEAD ZONE SURVIVAL

**Thể loại:** FPS / Hành động / Sinh tồn / Zombie

**Tagline:** *"Chào em, chào em, chào em đến với vùng chết."*

**Logline:** Năm 2031, một đại dịch zombie bùng phát tại thành phố Greenlake. Người chơi vào vai **Marcus Cole** — một cựu sĩ quan đặc nhiệm quân đội — thức dậy trong đống đổ nát của khu phố cổ với trí nhớ bị mất một phần. Mục tiêu: sinh tồn, tìm lại ký ức, giải cứu những người sống sót, và tìm đường thoát khỏi thành phố đã chết.

**Tổng quan gameplay:** Game kết hợp bắn súng góc nhìn thứ nhất (FPS) với yếu tố sinh tồn và khám phá. Người chơi phải quản lý tài nguyên (đạn, máu, thể lực), chiến đấu với nhiều loại zombie trong các đợt sóng (wave) ngày càng khó, đồng thời khám phá bản đồ để tìm vũ khí, vật phẩm và câu chuyện về thế giới đã sụp đổ.

**Nền tảng:** PC (Windows) — Unity Engine 2022 LTS

**Phong cách đồ họa:** Realistic stylized (giống Left 4 Dead, The Last of Us) — tạo hình nhân vật và môi trường chi tiết nhưng không hyper-realistic để giữ hiệu năng tốt.

**Đối tượng:** 18+ (nội dung bạo lực, khủng bố tâm lý)

---

# PHẦN II — LORE & CÂU CHUYỆN

## 2.1 Bối cảnh thế giới

### Thế giới hiện tại (2026–2031)

Năm 2026, một tập đoàn dược phẩm đa quốc gia tên **Helix BioSolutions** nghiên cứu một loại thuốc chữa ung thư mang tên **"Prometheus-7"**. Thuốc hoạt động bằng cách kích hoạt tái tạo tế bào cưỡng bức. Thử nghiệm giai đoạn 3 diễn ra tại **thành phố Greenlake** — một thành phố cảng trung bình ở miền Tây, dân số khoảng 340.000 người. Helix chọn nơi này vì quy định pháp lý lỏng lẻo và sự hợp tác của chính quyền địa phương.

### Sự cố (Ngày 0 — 14 tháng 3, 2031)

Khi thử nghiệm chuyển sang giai đoạn 4 (dùng trên bệnh nhân không phải ung thư), một lỗ hổng phát sinh: Prometheus-7 khiến hệ thống thần kinh của người chết não hoạt động trở lại, nhưng không khôi phục ý thức — chỉ có bản năng sơ khai: tấn công, cắn xé, lây nhiễm qua nước bọt.

Ngày 14/3, một bệnh nhân thử nghiệm chết não nhưng không ngờ vẫn còn hoạt động. Hắn cắn một y tá. Ba ngày sau, 12% dân số Greenlake đã biến thành zombie. Chính phủ tuyên bố thiết quân luật. Ngày 19/3, toàn bộ thành phố bị phong tỏa — không ai được ra, không ai được vào. Các đài truyền hình ngừng phát sóng vào ngày 23/3.

### Thời điểm game diễn ra (Ngày 47–52 sau Ngày 0)

Người chơi thức dậy vào ngày 47. Thành phố đã im lặng. Một số ít người sống sót trốn trong các điểm tập trung (safe house), cố gắng sinh tồn. Lực lượng quân đội được điều động nhưng đã rút lui sau khi thất bại trong việc kiểm soát. Helix BioSolutions đã biến mất — các lãnh đạo cao cấp rời đi bằng trực thăng vào ngày 21, để lại phòng thí nghiệm ngầm chứa đầy bằng chứng về sai phạm.

---

## 2.2 Lịch sử thành phố Greenlake

Greenlake được thành lập năm 1887 như một thị trấn khai thác gỗ. Đến thế kỷ 20, nó phát triển thành một thành phố cảng thương mại quan trọng. Đặc điểm:

- **Dân số:** 340.000 (trước Ngày 0)
- **Khí hậu:** Ôn đới, mùa đông lạnh, hay mưa
- **Địa hình:** Nằm bên bờ hồ lớn, có cảng, khu công nghiệp, khu dân cư, trung tâm thương mại, bệnh viện, trường đại học, và một nhà máy điện hạt nhân cũ (đã đóng cửa năm 2028)
- **Biểu tượng:** Tượng "Người đánh cá" ở bến cảng cũ — một phong cách art deco từ năm 1932

---

## 2.3 Các phe phái & tổ chức

### 1. Tàn dư Quân đội (Remnant Force)
Một tiểu đội 12 người còn sống sau cuộc triệt thoái, do **Đại úy Elena Vasquez** chỉ huy. Họ kiểm soát **Trạm cứu hỏa số 7** làm căn cứ. Mục tiêu: duy trì trật tự, bảo vệ dân thường, tìm cách liên lạc với bộ chỉ huy bên ngoài.

### 2. Nhóm y tế SOS (Survival Operations Squad)
Bác sĩ và y tá sống sót từ bệnh viện St. Margaret, do **Tiến sĩ James Park** dẫn dắt. Họ có nguồn thuốc men dồi dào nhưng thiếu vũ khí phòng thân. Họ bí mật nghiên cứu cách đảo ngược sự biến đổi của zombie.

### 3. Nhóm cướp "Blackout"
Một băng đảng tội phạm tổ chức dưới sự lãnh đạo của **Manuel "Shadow" Reyes** — trước đây là trùm ma túy địa phương. Họ chiếm **kho hàng cảng** làm hang ổ, cướp bóc những người sống sót khác. Họ có vũ khí nhưng không quan tâm đến việc cứu ai.

### 4. Người đơn độc (Lone Survivors)
Những cá nhân không theo phe, sống lay lắt trong các khu vực hoang vu. Một số điên loạn, một số giữ được lý trí. Họ có thể là đồng minh hoặc mối nguy hiểm.

### 5. Helix BioSolutions (Ẩn)
Công ty không biến mất hoàn toàn. Họ có một **phòng thí nghiệm bí mật dưới lòng thành phố** nơi họ tiếp tục nghiên cứu Prometheus-7 — với mục tiêu mới: biến zombie thành vũ khí sinh học kiểm soát được. **Tiến sĩ Helena Cross** — giám đốc nghiên cứu — vẫn ở đây, cùng với một nhóm nhỏ nhân viên trung thành.

---

## 2.4 Nhân vật chính

### Marcus Cole — Protagonist

**Tuổi:** 34 | **Nghề nghiệp cũ:** Trung sĩ đặc nhiệm, đơn vị chống khủng bố (đã xuất ngũ năm 2029 sau một sự cố trong nhiệm vụ)

**Ngoại hình:** Nam, cao 1m83, tóc nâu cắt ngắn quân đội, để râu lún phượng, có vết sẹo dài từ thái dương xuống gò má (bên phải). Thường mặc áo khoác da cũ màu olive, quần dù tactial, giày boots. Mắt xám lạnh, nhìn thẳng.

**Tính cách:** Cứng rắn, kỷ luật, ít nói, có trách nhiệm cao. Mất trí nhớ từng phần nên hay thất thần, tự hỏi mình đã làm gì trước khi tỉnh dậy. Có xu hướng hy sinh bản thân vì người khác — đặc biệt phụ nữ và trẻ em. Thích cà phê đen.

**Câu nói đặc trưng:** *"Nếu tôi nhớ được mình đã làm gì hôm đó, có lẽ tôi sẽ biết mình là ai."*

**Backstory đầy đủ:** Marcus Cole từng là thành viên của đơn vị đặc nhiệm Delta Foxtrot, tham gia nhiều chiến dịch ở Trung Đông. Năm 2029, trong một nhiệm vụ giải cứu con tin, đơn vị của anh bị phản bội bởi một nguồn tin nội bộ. 7/8 thành viên thiệt mạng. Marcus sống sót nhưng bị thương nặng. Sau khi xuất ngũ, anh trở về Greenlake — thành phố quê hương — làm bảo vệ cho Helix BioSolutions (công việc anh không nhớ rõ vì sao mình nhận, chỉ biết lương cao và ai đó đã giới thiệu qua một "người quen").

Ngày 14/3/2031, anh đang ở trong văn phòng Helix tầng 15 khi bệnh nhân đầu tiên biến đổi. Ký ức của anh bị gián đoạn từ thời điểm đó — anh không nhớ chuyện gì xảy ra trong 46 ngày tiếp theo. Vật duy nhất anh có là một **chìa khóa thẻ an ninh cấp cao** (Level 4) của Helix và một **tấm ảnh cũ** của mình bên cạnh một phụ nữ — phía sau ảnh có dòng chữ: *"Đừng quên chúng ta. — Sarah"*.

**Mối quan hệ với các phe phái:**
- Quân đội (Elena): Tôn trọng lẫn nhau vì cùng xuất thân. Elena cố gắng tuyển dụng anh.
- SOS (James): Hợp tác — James có thể giúp anh hiểu chuyện gì xảy ra với Helix.
- Blackout: Thù địch. Shadow biết Marcus từng làm bảo vệ Helix — và Shadow cần thông tin từ Helix.
- Helena Cross: Đối đầu — Helena biết Marcus đã thấy gì đó trong phòng thí nghiệm nhưng không nhớ.

### Tiến sĩ James Park — Bác sĩ

Bác sĩ lão lào 56 tuổi, chuyên khoa thần kinh. Người sáng lập nhóm SOS. Ông không phải chiến binh nhưng là người giữ cho nhóm tồn tại bằng y thuật và sự lạc quan có chủ đích. Ông nghiên cứu Prometheus-7 từ các mẫu vật và phát hiện ra: **sự biến đổi có thể đảo ngược** nếu được phát hiện sớm — nhưng để làm được điều đó, ông cần mẫu não của một zombie chưa hoàn toàn "chết".

### Elena Vasquez — Đại úy

Nữ sĩ quan 41 tuổi, gốc gác Hispanic, gia đình quân nhân ba thế hệ. Cô mất toàn bộ đơn vị trong cuộc triệt thoái và mang theo món nợ: đưa những người sống sót ra khỏi thành phố. Cô gặp Marcus ngày 48, tại khu dân cư. Cô nhận ra anh có kỹ năng chiến đấu xuất sắc và cố gắng thuyết phục anh gia nhập lực lượng quân đội tàn dư.

### Sarah Whitmore — Người trong ảnh

Vợ cũ của Marcus. Họ ly hôn năm 2030 sau một thời gian dài căng thẳng (liên quan đến PTSD của Marcus). Sarah sống ở khu phía Đông thành phố với con gái 7 tuổi tên **Lily**. Trước khi thành phố bị phong tỏa, Marcus định gọi điện cho Sarah — nhưng không bao giờ làm. Anh không biết cô có sống sót không.

---

## 2.5 Cốt truyện chính

### Mở đầu — Tỉnh dậy trong im lặng

Marcus tỉnh dậy trong một căn nhà hoang ở khu phố cổ. Ngoài cửa sổ, thành phố im lặng nhưng không phải im lặng yên bình — đó là im lặng của sự chết. Điện thoại anh không có sóng. TV chỉ còn static. Anh nhớ mình là ai, nhớ cách chiến đấu, nhưng 46 ngày vừa qua hoàn toàn trống rỗng.

Anh tìm thấy một **balô chiến thuật** gần đó với một khẩu M1911 (còn đạn), băng kit, và một tờ giấy ghi chữ: *"Tầng dưới. Tìm câu trả lời. — M.C."* — chính nét chữ của anh. Anh không nhớ viết điều này.

### Act 1 — Thức tỉnh (Ngày 47–48)

Marcus bắt đầu khám phá khu phố cổ. Đây là **Tutorial / Campaign đầu tiên**. Anh học lại cách chiến đấu, tiêu diệt zombie đầu tiên, tìm vũ khí tốt hơn.

Qua các điểm tham quan (journal entries, xác chết, graffiti), anh dần hiểu thành phố đã xảy ra chuyện gì. Anh tìm gặp **Elena Vasquez** gần Trạm cứu hỏa số 7. Elena cho anh biết: quân đội đã rút lui, Helix đã biến mất, và Helix chịu trách nhiệm cho mọi thứ.

Elena giao cho Marcus **Nhiệm vụ đầu tiên:** Cứu một nhóm dân thường mắc kẹt tại **Siêu thị Oakwood** — một điểm survival được cho là có khoảng 15 người, nhưng đã bị zombie bao vây 3 ngày.

Marcus thực hiện. Khi anh đến nơi, chỉ còn 4 người sống sót — và một trong số họ đã bị cắn. Họ yêu cầu Marcus giúp họ đến Trạm cứu hỏa. Trên đường đi, Marcus nhận ra mối de dọa thực sự không phải zombie mà là **nhóm Blackout** của Shadow — họ đang cướp các điểm survival.

### Act 2 — Những mảnh vỡ (Ngày 49–50)

Marcus được Elena giao nhiệm vụ tiếp theo: tìm nguồn cung cấp từ **Bệnh viện St. Margaret**, nơi **Tiến sĩ James Park** và nhóm SOS đang trú ẩn. James cần thuốc men; Elena cần Marcus để bảo vệ đoàn tiếp tế.

Khi Marcus đến bệnh viện, James cho anh xem các mẫu Prometheus-7 và phát hiện đáng lo ngại: **Helix không chỉ phát triển thuốc — họ đang thử nghiệm trên người mà không có sự đồng ý, và một số "bệnh nhân" đã biến đổi sớm hơn bất kỳ ai khác**.

Marcus bắt đầu nhớ lại những mảnh vỡ: anh từng thấy một căn phòng dưới tầng hầm Helix với những xác chết không bình thường. Anh không nhớ mình đã làm gì với thông tin đó.

Một đêm, khi Marcus đang nghỉ ngơi tại bệnh viện, nhóm Blackout tấn công. Họ muốn bắt James vì ông biết công thức Prometheus-7. Marcus chiến đấu bảo vệ bệnh viện, nhưng Shadow bắt được một điều quan trọng: **Marcus có thẻ Level 4 của Helix**. Shadow thề sẽ lấy nó.

### Act 3 — Sự thật (Ngày 51)

Marcus quyết định đột nhập **trụ sở Helix BioSolutions** — một tòa nhà văn phòng và phòng thí nghiệm ở trung tâm thành phố — để tìm câu trả lời. Với thẻ Level 4, anh có thể vào được khu vực giới hạn.

Bên trong, anh tìm thấy phòng thí nghiệm dưới lòng đất. Không chỉ là nhà kho — đây là **căn phòng điều khiển**. Màn hình cho thấy các camera giám sát khắp thành phố, một số vẫn hoạt động. Và có một **tường với ảnh bệnh nhân** — tất cả đều là người vô gia cư, tù nhân, và những người không ai tìm kiếm. Helix đã dùng họ làm chuột thí nghiệm.

Anh cũng tìm thấy một **nhật ký video** của Tiến sĩ Helena Cross ghi lại sự cố ngày 14/3: bệnh nhân đầu tiên không phải "tai nạn" — đó là **kết quả của việc ngừng thử nghiệm giai đoạn 3 đột ngột** do Helix muốn chuyển thẳng sang sản xuất thương mại. Họ đã bỏ qua các cảnh báo an toàn.

### Act 4 — Quyết định (Ngày 52)

Marcus trở về Trạm cứu hỏa với bằng chứng. Nhưng Elena có kế hoạch riêng: cô đã liên lạc được với một trực thăng quân đội bên ngoài vùng phong tỏa. Họ sẽ đến sơ cua trong 6 giờ. **Điều kiện:** Có tối đa 20 người sống sót tại điểm sơ cua.

Đây là lựa chọn cốt truyện:

**Kết thúc A — Hy sinh (The Greater Good):**
Marcus phát hiện Sarah và Lily vẫn còn sống ở khu Đông, nhưng để cứu họ, anh phải bỏ lại phần lớn nhóm SOS ở bệnh viện (không đủ thời gian để đi qua cả hai nơi). Elena khuyên anh đi cứu vợ con — nhưng James Park nài nỉ: *"Nếu không có bác sĩ, những người sống sót ra trực thăng sẽ chết vì thương tích không được điều trị."*

Marcus chọn đến bệnh viện trước. Anh cứu được nhóm SOS — bao gồm 2 trẻ em — nhưng khi quay lại khu Đông, ngôi nhà của Sarah trống rỗng. Có dấu hiệu họ đã rời đi. Marcus không biết họ còn sống hay đã chết.

**Kết thúc B — Cá nhân (The Personal War):**
Marcus đi cứu Sarah và Lily trước. Anh tìm thấy họ còn sống, đang trốn trong tầng hầm với một người đàn ông lạ mặt (một người sống sót không thuộc bất kỳ phe nào). Khi quay lại Trạm cứu hỏa, Elena và 4 người lính đã lên trực thăng rời đi — nhưng nhóm SOS ở bệnh viện bị Blackout tấn công. James Park thiệt mạng. Marcus không bao giờ biết liệu James có tìm được cách chữa hay không.

**Kết thúc C — Bất khả thi (The Impossible Choice):**
Marcus cố gắng làm cả hai — đến bệnh viện rồi chạy đến khu Đông. Đội Blackout biết kế hoạch của anh. Shadow chặn đường anh ở cầu cảng. Một trận đấu súng nổ ra. Marcus hạ được Shadow, nhưng bị trọng thương. Anh bò đến điểm sơ cua với Sarah và Lily, nhưng Elena nói với anh: *"Em xin lỗi. Trực thăng chỉ chở được 3 người nữa — chúng ta có 12. Ai đi?"* Trò chơi kết thúc ở đây, với một câu hỏi treo lơ lửng.

---

# PHẦN III — LORE BỔ SUNG

## 3.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| **Prometheus-7** | Loại thuốc gây ra đại dịch, kích hoạt tái tạo tế bào cưỡng bức |
| **Ngày 0** | Ngày 14/3/2031 — ngày bệnh nhân đầu tiên biến đổi |
| **Vùng chết (Dead Zone)** | Khu vực bị phong tỏa quanh Greenlake, không ai được ra vào |
| **Biến đổi (Turned)** | Quá trình một người bị cắn/bị lây nhiễm và trở thành zombie |
| **Người sống sót (Survivor)** | Con người không bị biến đổi, đang cố gắng sinh tồn |
| **Horde** | Một nhóm lớn zombie di chuyển cùng nhau |
| **Safe House** | Điểm tập trung của người sống sót, có thể nghỉ ngơi |
| **Sơ cua (Evac)** | Điểm di tản cuối cùng, nơi có thể rời khỏi thành phố |

## 3.2 Điểm tham quan & Easter Egg

- **Graffiti trên tường:** *"HELIX LIAR"* ở nhiều nơi — ai đó đã biết trước
- **Xác chết với áo đồng phục Helix** trong phòng thí nghiệm — họ đã thử nghiệm trên đồng nghiệp
- **Một căn nhà với ảnh gia đình không bị động đến** — có thể là của Sarah và Lily, có thể không
- **Radio cũ phát tín hiệu morse** trong khu công nghiệp — thông điệp: *"CROSS VẪN CÒN SỐNG — TẦNG NGẦM — CHẠY"*
- **Tượng Người đánh cá** ở bến cảng bị zombie dùng làm chỗ trú ẩn

## 3.3 Nhật ký ghi âm & Audio log

Các audio log rải rác trong map cho người chơi hiểu thêm về thế giới:

1. **Log #1 — James Park (Ngày 2):** *"Ngày thứ hai sau sự cố. Chúng tôi đã sơ tán được 23 người đến tầng 5. Bệnh viện có thể nuôi họ trong một tuần, không hơn. Tôi không hiểu Helix đã làm gì sai..."*

2. **Log #2 — Elena Vasquez (Ngày 8):** *"Lệnh triệt thoái là điên rồ. Họ đang bỏ rơi dân thường. Tôi ở lại. Ai đó phải ở lại."*

3. **Log #3 — Unknown (Ngày 15):** *[Tiếng thở hổn hển, tiếng bước chân]* *"Chúng đến rồi. Chào em, chào em, chào em..."* *[Tiếng đổ vỡ, tiếng la hét, rồi im lặng]*

4. **Log #4 — Helena Cross (Ngày 0 -14):** *"Prometheus-7 vượt qua mọi dự đoán. Chúng tôi đã sẵn sàng cho giai đoạn sản xuất. Ban giám đốc muốn thuốc trên kệ trong 6 tháng. Tôi đã báo cáo rủi ro, nhưng họ không nghe..."*

5. **Log #5 — Marcus Cole (Ngày 14, ghi âm từ điện thoại):** *[Giọng nói của Marcus, nghe như đang bị shock]* *"Tôi không... đây không phải... họ bảo tôi đóng cửa phòng B nhưng có tiếng hét từ bên trong. Tôi không... tôi đã mở... Sarah, nếu em nghe thấy... hãy mang Lily đi. Đi ngay. Đừng quay lại."*

---

# PHẦN IV — THẾ GIỚI & THIẾT KẾ LEVEL

## 4.1 Bản đồ thành phố

```
                    [BẾN CẢNG — HARBOR]
                          │
                    [KHU CÔNG NGHIỆP]
                    ══════════════
                         │
  [KHU Ổ CHUỘT]──[ĐẠI LỘ TRUNG TÂM]──[KHU TÀI CHÍNH]
       │                │                    │
  [NHÀ MÁY CŨ]    [TRUNG TÂM THƯƠNG MẠI]   [TRỤ SỞ HELIX]
       │                │                    │
  [KHU DÂN CƯ]    [KHU DÂN CƯ PHÍA BẮC]   [BỆNH VIỆN ST.MARGARET]
                      │                    │
        [KHU PHỐ CỔ — OLD TOWN]────────[TRẠM CỨU HỎA #7]
               │                    │
         [KHU DÂN CƯ]          [KHU ĐÔNG — EASTSIDE]
          (Start)               (Sarah's area)
```

## 4.2 Chi tiết từng khu vực

### Khu vực 1: Khu phố cổ (Old Town) — Tutorial / Act 1

**Mô tả:** Khu phố cổ với các tòa nhà thuộc đầu thế kỷ 20, đường phố hẹp, cửa hàng nhỏ, quán cà phê, và một quảng trường nhỏ. Đây là nơi Marcus tỉnh dậy. Kiến trúc Victorian pha trộn Art Deco.

**Gameplay:** Đây là tutorial zone. Người chơi học:
- Di chuyển cơ bản (WASD)
- Nhảy & chạy
- Ngắm & bắn
- Tương tác với vật thể
- Hệ thống loot cơ bản

**Zombie:** Chủ yếu Walker, số lượng ít. Phù hợp để người chơi tập bắn.

**Điểm tham quan:**
- Cửa hàng sách "Greenlake Books" — có audio log
- Quán cà phê "Morning Star" — có băng kit
- Quảng trường có tượng đài nhỏ — có súng shotgun (che giấu)

---

### Khu vực 2: Khu dân cư phía Bắc (Northside) — Act 1–2

**Mô tả:** Khu nhà ở trung lưu với biệt thự nhỏ, căn hộ, cửa hàng tiện lợi, trường tiểu học, và một nhà thờ nhỏ. Một số nhà còn nguyên vẹn, một số đã bị phá hủy. Đây là nơi có nhiều câu chuyện gia đình — đồ chơi trẻ em vung vãi, xe đạp trẻ em dựa tường, phòng ngủ với giường tầng.

**Gameplay:** Môi trường hỗn hợp: indoor và outdoor. Tường nhà có thể dùng làm cover. Nhiều điểm leo trèo (fence, car roof). Độ khó tăng dần.

**Zombie:** Walker + Runner bắt đầu xuất hiện. Zombie trong nhà có thể bất ngờ xuất hiện khi mở cửa.

**NPC:** Gặp **Elena Vasquez** ở đầu khu vực này.

**Điểm tham quan:**
- Nhà thờ St. Joseph — có xác một linh mục cầu nguyện với zombie đã đổ vỡ
- Trường tiểu học Greenlake — phòng học với bản đồ thế giới và ghế ngồi, có audio log của một giáo viên
- Cửa hàng tiện lợi "QuickStop" — loot tốt nhưng đã bị cướp trước đó

---

### Khu vực 3: Bệnh viện St. Margaret (Hospital) — Act 2

**Mô tả:** Bệnh viện đa khoa 8 tầng, thiết kế hiện đại (2015), với khoa cấp cứu, phòng mổ, khu vực bệnh nhân, và tầng hầm (nơi Helix bí mật làm thí nghiệm). Khu vực này tối tăm, ánh sáng chủ yếu từ cửa sổ và đèn khẩn cấp. Mùi chlorine và máu tanh.

**Gameplay:** Combat trong không gian hẹp. Nhiều phòng, hành lang, thang máy không hoạt động (phải dùng cầu thang). Một số phòng chứa item quý giá (thuốc, vũ khí), một số chứa zombie. Đặc biệt: **tầng hầm là khu vực cấm** — cần thẻ Level 3 để vào, Marcus có Level 4.

**Zombie:** Chủ yếu Crawler và Walker. Crawler hay ẩn nấp trong bóng tối, bất ngờ nhảy ra. Zombie bệnh viện mặc áo choàng bệnh nhân.

**NPC:** **Tiến sĩ James Park** và nhóm SOS.

**Điểm tham quan:**
- Khoa cấp cứu — có xác bệnh nhân bị trói vào giường (họ đã biến đổi)
- Phòng mổ — có thiết bị y tế vẫn hoạt động (ambient sound: monitor beeping)
- Tầng hầm — phòng thí nghiệm Helix, có camera an ninh ghi lại sự cố
- Tủ thuốc — nguồn băng kit (James cho phép)

---

### Khu vực 4: Trung tâm thương mại (Mall) — Act 2–3

**Mô tả:** Trung tâm thương mại lớn 3 tầng với hơn 60 cửa hàng, rạp chiếu phim, food court, và một tầng hầm làm bãi đỗ xe. Trước khi đại dịch, đây là nơi đông đúc nhất thành phố. Giờ đây, nó trông như một xác khổng lồ: cửa kính vỡ, thang cuốn đứng im, gian hàng trưng bày đổ nát.

**Gameplay:** Combat đa tầng. Người chơi có thể di chuyển giữa các tầng bằng thang cuốn và cầu thang. Môi trường phong phú với nhiều loại cover. Vertical gameplay quan trọng — zombie có thể xuất hiện từ tầng trên.

**Zombie:** Tất cả loại trừ Brute. Số lượng lớn. Nhiều Horde trigger (âm thanh lớn, ví dụ: bắn trúng bình thủy tinh).

**Loot:** Tốt nhất trong game — nhiều vũ khí, đạn, item hiếm.

**Điểm tham quan:**
- Cửa hàng súng "Black River Arms" — khóa cần key, bên trong có Assault Rifle và nhiều đạn
- Rạp chiếu phim — có thể vào xem một cảnh zombie trên màn hình
- Khu vực trẻ em — có sân chơi với xác một người mẹ ôm con

---

### Khu vực 5: Trụ sở Helix BioSolutions (Helix Tower) — Act 3

**Mô tả:** Tòa nhà văn phòng 18 tầng + 4 tầng hầm, thiết kế hiện đại, glass-and-steel. Lối vào chính bị chặn (xe tải đổ), phải vào bằng đường garage tầng hầm. Bên trong: văn phòng sang trọng nhưng đổ nát, phòng họp với bảng trắng đầy công thức, và tầng hầm với phòng thí nghiệm sinh học.

**Gameplay:** Stealth + Combat hybrid. Nhiều camera an ninh vẫn hoạt động (gây alert nếu đi vào vùng). Zombie bảo vệ (security) có áo đồng phục Helix. Khu vực tầng hầm cần thẻ Level 4 để vào — Marcus có thể vào mọi nơi.

**Zombie:** Security zombie (mặc đồng phục, có baton điện), Researcher zombie (mặc áo blouse trắng), và 1 **Boss zombie: Security Chief "Bulwark"** — một gã to lớn với áo giáp chống bạo động (HP cao, shield).

**Điểm tham quan:**
- Tầng 15 (văn phòng Marcus) — có desk với ảnh Sarah, có thể tìm thấy gợi ý về ký ức
- Phòng họp hội đồng quản trị — bảng trắng với dòng: *"PRODUCTION BY ANY MEANS NECESSARY — DATE: 03/13/2031"*
- Tầng hầm 4 — phòng thí nghiệm chính, màn hình cho thấy video ghi hình sự cố
- Server room — có máy tính với dữ liệu đầy đủ về Prometheus-7

---

### Khu vực 6: Bến cảng & Kho hàng (Harbor) — Act 4

**Mô tả:** Khu cảng công nghiệp với kho hàng container, cầu cảng, tàu chở hàng bị bỏ hoang, và nhà kho cũ. Đây là lãnh thổ của **Blackout**. Không khí mặn và dầu nhớt. Nhiều container có thể trèo lên, tạo thành mê cung.

**Gameplay:** Combat intense nhất. Nhiều Horde. Snipers của Blackout trên nóc kho hàng. Người chơi phải cẩn thận di chuyển giữa các container. Nhiều ambush point.

**Zombie:** Tất cả loại + **Brute** xuất hiện ở đây. Brute hoạt động như boss mini — xuất hiện khi người chơi đến gần kho container số 7.

**NPC:** Thành viên Blackout — có thể đàm phán hoặc chiến đấu. **Shadow Reyes** xuất hiện ở đây (boss encounter).

**Điểm tham quan:**
- Tàu "MS Aurora" — tàu chở hàng bị bỏ, có thể tìm thấy vũ khí nặng (grenade launcher prototype — lore)
- Container "HC-7749" — khóa, bên trong có nhiều mẫu Prometheus-7
- Văn phòng cảng với bản đồ thành phố có vùng phong tỏa được đánh dấu

---

### Khu vực 7: Trạm cứu hỏa số 7 (Fire Station #7) — Hub & Act 4

**Mô tả:** Trạm cứu hỏa 2 tầng với garage, phòng ngủ, phòng ăn, và sân thượng. Đây là **hub chính** của game — nơi người chơi quay về giữa các nhiệm vụ. Có thể nghỉ ngơi, xem inventory, nghe radio, và giao tiếp với NPC.

**Gameplay:** Safe zone. Không có zombie. Người chơi có thể:
- Nói chuyện với NPC để hiểu thêm câu chuyện
- Xem bản đồ và chọn nhiệm vụ tiếp theo
- Lưu game (checkpoint)
- Crafting & upgrade

**NPC:** Elena Vasquez (luôn ở đây), các thành viên tàn dư quân đội, và dân thường sống sót.

**Điểm tham quan:**
- Phòng ăn — bảng thông báo với danh sách người mất tích (một số tên có thể quen)
- Garage — xe cứu hỏa vẫn hoạt động (nhưng không có nhiên liệu)
- Sân thượng — nhìn toàn cảnh thành phố, có thể thấy điểm sơ cua

---

### Khu vực 8: Khu Đông (Eastside) — Act 4, Kết thúc

**Mô tả:** Khu dân cư cũ với nhà phố liền kề, cửa hàng nhỏ, công viên nhỏ, và một trường mẫu giáo. Đây là khu vực Sarah và Lily trú ẩn. Cách Trạm cứu hỏa khoảng 15 phút chạy bộ — nhưng giữa đường là lãnh thổ Blackout.

**Gameplay:** Phụ thuộc vào lựa chọn cốt truyện. Nếu đi cứu Sarah: stealth nặng (tránh Blackout), ít zombie. Nếu không: đây là khu vực survival với wave zombie.

**Điểm tham quan:**
- Ngôi nhà của Sarah — có thể nhận ra từ ảnh, có đồ chơi của Lily, có vết máu trên sàn (nhưng không chắc chắn là ai)
- Công viên — xích đu vẫn đung đưa dù không có gió

---

### Điểm sơ cua (Evacuation Point)

**Mô tả:** Sân helipad trên nóc tòa nhà chính quyền thành phố, gần trung tâm thương mại. Đây là điểm cuối cùng của game. Trực thăng UH-60 Black Hawk sẽ đến. Người chơi phải sống sót trong 3 phút wave cuối trong khi chờ trực thăng.

**Gameplay:** Wave defense cuối cùng. Tất cả loại zombie xuất hiện. Brute có thể xuất hiện 2 lần. Người chơi phải quản lý vị trí, đạn dược, và thời gian.

---

# PHẦN V — HỆ THỐNG GAMEPLAY

## 5.1 Điều khiển

### Desktop (PC)

| Hành động | Phím mặc định |
|---|---|
| Di chuyển | WASD |
| Nhảy | Space |
| Chạy | Left Shift (giữ) |
| Ngồi xổm / Lăn | Left Ctrl |
| Ngắm súng | Chuột phải (Hold) |
| Bắn | Chuột trái |
| Nạp đạn | R |
| Đổi vũ khí nhanh | Q (prev) / E (next) |
| Số 1–5 | Chọn vũ khí trực tiếp |
| Tương tác / Nhặt đồ | F |
| Grenade | G |
| Dùng item (băng kit) | H |
| Mở inventory | Tab |
| Bản đồ | M |
| Menu tạm dừng | Escape |

---

## 5.2 Hệ thống vũ khí

| Tên | Loại | Damage | Tốc độ bắn | Mag size | Reload | Đặc điểm |
|---|---|---|---|---|---|---|
| **M1911** | Pistol | 25 | 400 RPM | 7+1 | 1.8s | Vũ khí khởi đầu. Reliable, không có recoil. |
| **Remington 870** | Shotgun | 80×8 (pellet) | 60 RPM | 4+1 | 2.5s | Súng đạn rải. Hiệu quả cực cao ở tầm gần. |
| **M4A1 Carbine** | Assault Rifle | 30 | 700 RPM | 30+1 | 2.3s | Vũ khí balanced. Tốt ở mọi tầm. |
| **AWP** | Sniper Rifle | 150 | 40 RPM | 5+1 | 3.5s | Một phát chết hầu hết zombie. Scope 4×. |
| **MP5** | SMG | 20 | 800 RPM | 30+1 | 2.0s | Tốc độ bắn cực nhanh. Damage thấp. |
| **Molotov** | Grenade | 60 DoT | — | 3 max | — | Sát thương theo thời gian trong vùng. |
| **Frag Grenade** | Grenade | 100 + 50 splash | — | 5 max | — | Sát thương diện rộng. Thu hút Horde. |

### Nâng cấp vũ khí (Crafting)

| Level | Tên | Yêu cầu | Hiệu ứng |
|---|---|---|---|
| 0 | Stock | — | Mặc định |
| 1 | Refurbished | 10 scrap + 2 circuits | +10% damage, -5% recoil |
| 2 | Custom | 25 scrap + 5 circuits + 1 weapon part | +20% damage, -10% recoil, +2 mag size |
| 3 | Elite | 50 scrap + 10 circuits + 3 weapon parts | +30% damage, -20% recoil, +5 mag size, faster reload |

---

## 5.3 Hệ thống sinh tồn

### Máu (Health)

- **Giá trị:** 100 HP
- **Mất máu:** Khi bị zombie tấn công (tùy loại: 10–40 damage)
- **Hồi phục tự nhiên:** +2 HP/giây khi không nhận sát thương trong 5 giây
- **Hồi phục nhanh:** Băng kit hồi 50 HP (3 giây channel, có thể bị gián đoạn)
- **Chết:** Khi HP <= 0 → Game Over screen → Restart from checkpoint

### Thể lực (Stamina)

- **Giá trị:** 100 stamina
- **Tiêu hao:**
  - Chạy: -20/giây
  - Nhảy: -15/lần nhảy
  - Lăn/ngồi xổm: -5/giây
- **Hồi phục:** +15/giây khi đi bộ hoặc đứng yên
- **Người chơi không thể chạy khi stamina = 0**

### Túi đạn

- **Mỗi vũ khí có 2 nguồn đạn:**
  - **Magazine (Băng đạn):** Đạn trong băng hiện tại
  - **Reserve (Dự trữ):** Đạn mang theo người
- **Tổng dự trữ ban đầu:** 60 viên (pistol), tăng khi nhặt thêm
- **Khi hết đạn dự trữ:** Không thể nạp đạn (buộc phải chuyển sang vũ khí khác hoặc tìm đạn)

---

## 5.4 Hệ thống zombie

### Zombie thường (Walker)

- **HP:** 50 | **Damage:** 10/hit | **Tốc độ:** 2 m/s
- **AI:** State machine đơn giản — patrol → chase → attack
- **Tầm phát hiện:** 20m (thị giác), 15m (thính giác)
- **Hành vi:** Đi bộ chậm, tấn công khi đến gần. Không thể leo thang, nhưng có thể nhảy từ độ cao thấp.
- **Visual:** Da xanh lục, mắt trắng đục, quần áo dân thường rách nát.

### Zombie nhanh (Runner)

- **HP:** 30 | **Damage:** 15/hit | **Tốc độ:** 6 m/s
- **AI:** Luôn luôn chase, không patrol. Thông minh hơn Walker — có thể dự đoán đường chạy của người chơi.
- **Tầm phát hiện:** 30m (thị giác), 25m (thính giác)
- **Hành vi:** Lao thẳng tới người chơi, không né tránh. Bỏ qua một số vật cản thấp.
- **Visual:** Gầy, cơ bắp căng, đôi mắt đỏ, móng tay dài. Mặc đồ thể thao.

### Zombie khổng lồ (Brute)

- **HP:** 200 | **Damage:** 40/hit | **Tốc độ:** 1.5 m/s
- **AI:** Territorial — đứng yên trong khu vực, chỉ chase khi người chơi vào tầm 15m.
- **Khả năng đặc biệt:**
  - **Ground Slam:** Đập tay xuống đất, tạo sóng chấn động làm người chơi bị stun 0.5s trong bán kính 5m
  - **Roar:** Gầm lên, thu hút mọi zombie trong bán kính 50m đến vị trí của hắn
- **Hành vi:** Chỉ xuất hiện ở khu vực cố định (Brute Spawn Points). Khi Brute chết, không respawn.
- **Visual:** 2.5m chiều cao, cơ bắp quá khổ, da nâu xám, quần áo công nhân. Để lại **Brute Trophy** khi chết.

### Zombie tàng hình (Crawler)

- **HP:** 20 | **Damage:** 8/hit | **Tốc độ:** 4 m/s (bò), 7 m/s (lai tới)
- **AI:** Predator. Crawler ẩn trong bóng tối, chờ người chơi đi qua. Kích hoạt khi người chơi trong bán kính 5m.
- **Khả năng đặc biệt:**
  - **Stealth:** Gần như không có tiếng động. Khó phát hiện bằng thính giác.
  - **Pounce:** Khi ở trong bán kính 3m, nhảy bổ xuống người chơi, gây 20 damage + knockback
- **Hành vi:** Luôn ẩn nấp khi có thể. Di chuyển bằng 4 chân. Thường xuất hiện trong nhà, bệnh viện, kho hàng.
- **Visual:** Bò bằng 4 chi, lưng gù, da nhợt nhạt. Quần áo bệnh nhân hoặc đồ ngủ.

### Zombie bảo vệ (Security Zombie)

- **HP:** 80 | **Damage:** 20/hit | **Tốc độ:** 3 m/s
- **AI:** Guard — di chuyển theo pattern cố định, patrol giữa các điểm.
- **Khả năng đặc biệt:**
  - **Baton:** Vũ khí melee gây stun ngắn (0.3s)
- **Hành vi:** Chỉ xuất hiện trong khu vực Helix.
- **Visual:** Đồng phục bảo vệ Helix màu đen, baton điện.

### Zombie báo động (Screamer)

- **HP:** 40 | **Damage:** 5/hit | **Tốc độ:** 3 m/s
- **AI:** Suicide bomber. Khi nhìn thấy người chơi, chạy tới và **hét lên** trước khi tấn công.
- **Khả năng đặc biệt:**
  - **Alert Scream:** Gây alert cho TẤT CẢ zombie trong bán kính 80m. Đây là mối nguy hiểm lớn.
- **Hành vi:** Đứng yên cho đến khi phát hiện người chơi, sau đó lao tới.
- **Visual:** Miệng rộng bất thường, yết hầu phồng to, mắt mở to.

---

## 5.5 Hệ thống Wave

| Wave | Zombie | Số lượng | Ghi chú |
|---|---|---|---|
| 1 | Walker | 5 | Tutorial wave |
| 2 | Walker | 8 | |
| 3 | Walker | 12 | |
| 4 | Walker + Runner | 10+3 | Runner xuất hiện |
| 5 | Walker + Runner | 12+5 | |
| 6 | Walker + Runner | 15+8 | |
| 7 | Walker + Runner + Crawler | 10+5+3 | Crawler xuất hiện |
| 8 | Walker + Runner + Crawler | 12+8+5 | |
| 9 | Walker + Runner + Crawler + Screamer | 15+8+5+2 | Screamer xuất hiện |
| 10+ | Tất cả loại | +10%/wave | Brute spawn (1 per 3 waves) |

---

## 5.6 Hệ thống Loot

| Tier | Màu | Tỷ lệ rơi | Ví dụ |
|---|---|---|---|
| **Common** | Xám | 50% | Đạn pistol (10), băng kit nhỏ |
| **Uncommon** | Xanh lá | 30% | Đạn shotgun (4), băng kit lớn, Medkit |
| **Rare** | Xanh dương | 15% | Vũ khí (MP5, M4A1), túi đạn lớn |
| **Epic** | Tím | 4% | Vũ khí hiếm (AWP), attachment |
| **Legendary** | Cam | 1% | Weapon blueprint, Elite upgrade kit |

---

# PHẦN VI — NHIỆM VỤ (MISSIONS)

## 6.1 Nhiệm vụ chính (Main Story)

**ACT 1:**
- **M1:** Thoát khỏi căn nhà hoang — Tutorial
- **M2:** Tìm vũ khí tại Old Town
- **M3:** Gặp Elena Vasquez
- **M4:** Cứu dân thường tại Siêu thị Oakwood
- **M5:** Đánh bại Horde đầu tiên (Wave 1–3)

**ACT 2:**
- **M6:** Đến Bệnh viện St. Margaret
- **M7:** Bảo vệ đoàn tiếp tế (Convoy mission)
- **M8:** Khám phá tầng hầm bệnh viện
- **M9:** Chống đỡ cuộc tấn công của Blackout
- **M10:** Thu thập bằng chứng về Prometheus-7

**ACT 3:**
- **M11:** Đột nhập Trụ sở Helix
- **M12:** Xâm nhập tầng hầm
- **M13:** Đối đầu Security Chief (Boss fight)
- **M14:** Trở về Trạm cứu hỏa với bằng chứng

**ACT 4:**
- **M15:** Gọi trực thăng sơ cua
- **M16:** Wave cuối cùng tại điểm sơ cua
- **M17:** Lựa chọn kết thúc (A/B/C)
- **M18:** Cutscene kết thúc

## 6.2 Nhiệm vụ phụ (Side Quests)

| ID | Tên | Người giao | Mô tả | Phần thưởng |
|---|---|---|---|---|
| **SQ1** | "Người hàng xóm tốt" | Elena | Tìm 5 bức thư của một gia đình trước Ngày 0, rải khắp Old Town | 50 XP + Keycard |
| **SQ2** | "Y tá đêm" | James | Tìm nhật ký của một y tá đêm trong bệnh viện | 30 XP + Medkit recipe |
| **SQ3** | "Radio của Tom" | — | Tìm radio cổ của một cậu bé trong trường tiểu học, bật lên nghe audio log | 20 XP |
| **SQ4** | "Thùng hàng" | — | Tìm 3 thùng hàng Helix bị mất trong kho cảng | 40 XP + Weapon part |
| **SQ5** | "Đường tắt" | Elena | Mở khóa 2 lối tắt trên bản đồ bằng cách giải cứu 2 người sống sót bị mắc kẹt | 60 XP + Access to shortcuts |
| **SQ6** | "Trả thù" | Elena | Tiêu diệt 3 trưởng điểm của Blackout | 80 XP + Assault Rifle |
| **SQ7** | "Âm thanh cuối cùng" | — | Tìm đài phát thanh địa phương, bật lên nghe tin tức Ngày 0 | 25 XP |
| **SQ8** | "Bảo tàng" | — | Tìm 10 hiện vật trong trung tâm thương mại (collectible) | 70 XP + Legendary weapon |

## 6.3 Thiết kế nhiệm vụ chi tiết

### M1 — Thoát khỏi căn nhà hoang (Tutorial)

**Mục tiêu:**
1. Wake up — Tương tác với cửa (F)
2. Tìm hiểu di chuyển — Đi ra phòng khách
3. Nhặt khẩu M1911 — Trên bàn
4. Tương tác với cửa sổ — Xem cutscene giới thiệu
5. Di chuyển đến cửa trước — Trong khi đó, 1 Walker xuất hiện
6. Tiêu diệt Walker — Hướng dẫn bắn súng
7. Rời khỏi căn nhà

**HUD Tutorial Popup:** Lần lượt hiện hướng dẫn WASD, Space, Chuột trái, Chuột phải khi người chơi đến đúng điểm.

**Fail condition:** Không có — Walker không thể giết người chơi (sẽ đánh 1 hit rồi dừng, để tutorial).

---

### M4 — Cứu dân thường tại Siêu thị Oakwood

**Setup:** Elena giao nhiệm vụ. Trên đường đến siêu thị, người chơi phải chiến đấu với 2 wave.

**Mục tiêu:**
1. Đến siêu thị Oakwood (checkpoint)
2. Tiêu diệt zombie bên ngoài (Wave 1: 8 Walker)
3. Vào bên trong — bất ngờ: 3 Crawler ẩn trong bóng tối
4. Tìm kiếm 4 survivor trong 3 tầng siêu thị
   - Tầng 1: 1 survivor (bị kẹt trong phòng kho)
   - Tầng 2: 2 survivor (bị kẹt trong khu vực thực phẩm)
   - Tầng 3: 1 survivor (bị cắn, sắp biến đổi)
5. Quyết định: Giết người bị cắn (thương xót) hay để họ biến đổi?
6. Dẫn survivor ra ngoài
7. Trên đường về, bị Blackout ambush — chiến đấu với 4 gang member
8. Về đến Trạm cứu hỏa

**Loot reward:** 1 Weapon part, 30 scrap, 1 grenade

---

### M13 — Đối đầu Security Chief "Bulwark" (Boss Fight)

**Setup:** Marcus đến tầng hầm 4 của Helix Tower. Một con zombie khổng lồ đứng chắn lối ra.

**Boss Fight: Bulwark**

- **HP:** 500
- **Shield:** 200 (phục hồi nếu không tấn công trong 10s)
- **Damage:** 50/hit
- **Tốc độ:** 2 m/s

**Pattern chiến đấu:**

| Phase | HP | Hành vi |
|---|---|---|
| **Phase 1** (500–350 HP) | | Di chuyển chậm, đánh swing chậm. Shield active. Có thể stun bằng headshot. |
| **Phase 2** (350–200 HP) | | Shield vỡ. Tốc độ tăng 30%. Thêm ground slam attack. Roar gọi 2 Security Zombie. |
| **Phase 3** (200–0 HP) | | Rage mode. Tốc độ tăng 50%. Đánh liên tục. Đèn nhấp nháy. HP bar màu đỏ. |

**Chiến thuật:**
- Dùng cover trong phòng thí nghiệm (bàn, tủ, cột)
- Phá shield bằng shotgun → headshot khi shield down
- Khi rage: di chuyển liên tục, không đứng yên
- Grenade gây 150 splash damage — dùng khi HP còn 200

**Reward:** Brute Trophy + Elite Weapon Part + Helix Access Card → mở mọi cửa trong game.

---

# PHẦN VII — THIẾT KẾ UI/UX

## 7.1 HUD (Màn hình trong game)

```
┌─────────────────────────────────────────────────────────────────┐
│                    [WAVE 5 — 15 ZOMBIES LEFT]                    │
│                                                                  │
│                                                                  │
│                                                                  │
│                        [INTERACTION: F]                          │
│                             (●)                                  │
│                                                                  │
│                                                                  │
│ [♥ ████████████░░░] 100/100 HP     [M4A1]  [24/90]  [GRENADE ×2] │
│ [⚡ ██████░░░░░░░] 60/100 STAMINA  [Q]Swap                        │
│                                                                  │
│ [MAP] ← M key                                    [MINIMAP]       │
│                                                 ┌──────────┐     │
│                                                 │    ↑     │     │
│                                                 │  ← ● →   │     │
│                                                 │    ↓     │     │
│                                                 └──────────┘     │
└─────────────────────────────────────────────────────────────────┘
```

### Chi tiết từng phần tử

| Phần tử | Vị trí | Mô tả |
|---|---|---|
| **Wave Counter** | Trên cùng, giữa | "WAVE X — Y ZOMBIES LEFT". Font to, màu trắng đỏ nhạt. Fade khi không có zombie. |
| **Crosshair** | Chính giữa | Chấm tròn nhỏ, màu trắng. Thu nhỏ 50% khi ngắm. Đỏ khi nhắm trúng zombie. |
| **Health Bar** | Dưới trái | Thanh ngang, màu đỏ (#E53935). Có icon trái tim. Số cụ thể ở bên phải. Chớp đỏ khi HP < 25%. |
| **Stamina Bar** | Dưới health bar | Thanh ngang, màu vàng (#FDD835). Icon lightning bolt. Mất khi chạy. |
| **Weapon Display** | Dưới phải | Tên vũ khí + icon. Số đạn trong mag / reserve. Tự động hiển thị khi đổi súng. |
| **Grenade Counter** | Dưới weapon | Icon grenade + số lượng |
| **Interaction Prompt** | Chính giữa (dưới crosshair) | "Press F" khi có vật tương tác trong tầm. Font trắng, có outline. |
| **Mini-map** | Góc trên phải | Bán kính 100m, xoay theo hướng nhìn. Zombie là chấm đỏ. NPC là chấm xanh lá. Loot là chấm vàng. |
| **Damage Indicator** | Quanh crosshair | Mũi tên đỏ chỉ hướng bị tấn công |
| **Hit Marker** | Chính giữa | "X" trắng nhỏ xuất hiện 0.2s khi bắn trúng |
| **Kill Feed** | Trên phải (dưới minimap) | "[Loại zombie] eliminated" — hiện 2s rồi fade |

## 7.2 Menu

### Main Menu

```
════════════════════════════════════════════════════
          ╔═══════════════════════════╗
          ║   DEAD ZONE SURVIVAL       ║
          ║   ─────────────────        ║
          ║                             ║
          ║      ▶ NEW GAME            ║
          ║        CONTINUE             ║
          ║        SETTINGS            ║
          ║        CREDITS             ║
          ║        QUIT                ║
          ║                             ║
          ╚═══════════════════════════╝

  [Background: Ảnh bến cảng Greenlake lúc hoàng hôn,
   có bóng đen của một zombie đứng ở xa]
```

### Pause Menu

```
┌──────────────────────────────────────┐
│           ⏸ PAUSED                    │
│                                      │
│         ▶ RESUME                      │
│           RESTART MISSION             │
│           SETTINGS                    │
│           CONTROLS                    │
│           QUIT TO MAIN MENU           │
│                                      │
│  [HUD vẫn hiển thị mờ phía sau]      │
└──────────────────────────────────────┘
```

### Inventory Screen

```
┌─ WEAPONS ──────────────────────────────────────────────────────┐
│  [1] M4A1 Carbine       Damage: 30  Mag: 30  [ĐANG TRANG BỊ]   │
│  [2] M1911              Damage: 25  Mag: 7                     │
│  [3] Remington 870       Damage: 80  Mag: 4                      │
│  [4] — Chỗ trống —                                               │
│  [5] — Chỗ trống —                                               │
└─────────────────────────────────────────────────────────────────┘
┌─ ITEMS ────────────────────────────────────────────────────────┐
│  [H] Medkit (Lớn)             ×3                                 │
│  [G] Lựu đạn Frag            ×2                                 │
│  [G] Molotov                 ×1                                 │
│  Stamina Drink               ×1                                 │
└─────────────────────────────────────────────────────────────────┘
┌─ NGUYÊN LIỆU ──────────────────────────────────────────────────┐
│  Scrap: 45      Circuits: 12      Weapon Parts: 3               │
└─────────────────────────────────────────────────────────────────┘
┌─ CHẾ TẠO ─────────────────────────────────────────────────────┐
│  [Nâng cấp M4A1 → Cấp 1]  10 Scrap + 2 Circuits  [CHẾ TẠO]   │
│  [Chế Medkit]              5 Scrap + 1 Circuits   [CHẾ TẠO]   │
└─────────────────────────────────────────────────────────────────┘
```

## 7.3 Hệ thống hội thoại

Khi tương tác với NPC, màn hình chuyển sang **Dialog Mode**:

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                      │
│  [Portrait: Elena Vasquez — Biểu cảm trung lập]                     │
│                                                                      │
│  ELENA VASQUEZ                                                       │
│  ─────────────────                                                   │
│  "Marcus, ta cần nói chuyện. Có chuyện ở Oakwood Mall.           │
│   Một nhóm người mắc kẹt ở đó. Chúng ta phải giúp họ."             │
│                                                                      │
│         ┌──────────────────┐  ┌──────────────────┐                 │
│         │ "Tôi sẽ đi ngay."│  │ "Họ có thể tự    │                 │
│         │ [Đồng ý]          │  │  lo cho bản thân."│                 │
│         └──────────────────┘  └──────────────────┘                 │
│                                                                      │
│  ┌─ UY TÍN ──────────────────────────────────────────────────────┐ │
│  │  Elena: ████████░░ (Thân thiện)                                │ │
│  └─────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

---

# PHẦN VIII — THIẾT KẾ AUDIO

## 8.1 Nhạc nền (Music)

### Theme chính (Main Theme)
- **Cảm xúc:** Bất lực, cô đơn, nhưng có hy vọng le lói
- **Nhạc cụ:** Piano đơn độc + string orchestra + ambient drone
- **Tham chiếu:** Giống "The Last of Us" main theme — tối giản nhưng xúc động

### Phong cách nhạc theo tình huống

| Tình huống | Phong cách | Mô tả |
|---|---|---|
| **Menu / Hub** | Atmospheric ambient | Âm thanh môi trường thành phố chết (gió, kẽt cửa, xa xa có tiếng động lạ) |
| **Khám phá (Exploration)** | Tense ambient | Nhạc du dương nhẹ, âm vực thấp, tension building khi đến gần zombie |
| **Combat nhẹ (1–3 zombie)** | Combat tension | Drum beat nhanh dần, string section, tạo cảm giác nguy hiểm |
| **Combat nặng (Horde)** | Full combat | Orchestral battle music, brass mạnh, percussion dữ dội |
| **Boss Fight (Bulwark)** | Boss theme | Nặng nề, industrial, bass rumble, tiếng kim loại đập |
| **Cutscene** | Cinematic | Tùy nội dung — emotional piano cho cảnh buồn, tension strings cho cảnh kinh dị |
| **Kết thúc** | Emotional | Tùy kết thúc — A (hy sinh, bittersweet), B (mất mát, dark), C (treo lơ lửng, empty) |

## 8.2 Hiệu ứng âm thanh (SFX)

### Âm thanh vũ khí

| Súng | Âm thanh bắn | Âm thanh nạp đạn |
|---|---|---|
| M1911 | Tiếng nổ nhỏ, khô, đặc trưng | Tiếng clip out/in, cò + slide |
| Remington 870 | Tiếng nổ lớn, vang, bass | Tiếng shell eject, pump action |
| M4A1 | Tiếng nổ liên tục, auto, military | Tiếng mag drop, mag in, charging |
| AWP | Tiếng nổ cực lớn, echo dài | Tiếng bolt action |
| MP5 | Tiếng nổ nhanh, auto, nhỏ hơn M4 | Tiếng mag change |

### Âm thanh zombie

| Loại zombie | Tiếng di chuyển | Tiếng tấn công | Tiếng đặc biệt |
|---|---|---|---|
| Walker | Bước chân nặng nề, kéo lê | Gầm thấp, tiếng xé thịt | — |
| Runner | Bước chạy nhanh, hơi thở | Gầm cao, hung dữ | — |
| Crawler | Gần như im lặng | Rít nhẹ, nhanh | — |
| Brute | Bước chân rung chuyển, nặng nề | Gầm rống, tiếng đập | Tiếng ground slam |
| Screamer | Bước chạy + thở hổn hển | — | **Tiếng hét** (rất lớn, kinh hoàng) |

### Môi trường

| Âm thanh | Mô tả |
|---|---|
| Gió | Biến đổi theo thời gian trong ngày |
| Mưa | Tiếng rơi, có thể che dấu bước chân người chơi |
| Chim | Hiếm, khi nghe được nghĩa là khu vực an toàn |
| Tiếng rơi đổ | Vật thể rơi trong tòa nhà hoang |
| Kẽt cửa | Mở cửa, đóng cửa |
| Bước chân trên bề mặt | Khác nhau: bê tông, kính vỡ, nước, gỗ |
| Radio static | Khi bật radio cũ |

## 8.3 Giọng nói nhân vật (Voice)

| Nhân vật | Giọng | Đặc điểm |
|---|---|---|
| Marcus Cole | Nam trung niên, giọng trầm, American accent | Nói ít, câu từ ngắn gọn. Khi bắn: *"Contact!"*. Khi chết: *"No... not yet..."* |
| Elena Vasquez | Nữ, 30–40s, giọng lạnh, command tone | Nói ngắn gọn, quân đội. *"We don't have time."* |
| James Park | Nam lớn tuổi, giọng nhẹ nhàng, lo lắng | Nói dài hơn, ân cần. *"Be careful out there."* |
| Shadow Reyes | Nam, 30s, giọng đe dọa, Latin accent | Đe dọa. *"Your card or your life, soldier."* |
| Helena Cross | Nữ, 40s, giọng lạnh, calculated | Giọng khoa học, không cảm xúc. *"You shouldn't have come here."* |

---

# PHẦN IX — HỆ THỐNG KỸ THUẬT

## 9.1 Kiến trúc code

### Cấu trúc thư mục Scripts

```
Assets/Scripts/
├── Player/
│   ├── PlayerController.cs       — Di chuyển, nhảy, chạy, ngồi
│   ├── PlayerCombat.cs           — Bắn súng, nạp đạn, damage
│   ├── PlayerStats.cs            — HP, stamina, inventory
│   ├── PlayerInteraction.cs       — Tương tác với vật thể, NPC
│   ├── PlayerFOV.cs               — Camera, ngắm, zoom
│   └── PlayerAudio.cs             — Bước chân, thở, grunt
├── Enemies/
│   ├── ZombieBase.cs              — Base class cho tất cả zombie
│   ├── ZombieWalker.cs           — Walker AI
│   ├── ZombieRunner.cs           — Runner AI
│   ├── ZombieBrute.cs             — Brute AI + ground slam
│   ├── ZombieCrawler.cs          — Crawler AI + stealth
│   ├── ZombieSecurity.cs         — Security zombie AI
│   ├── ZombieScreamer.cs          — Screamer AI + alert
│   ├── EnemyManager.cs           — Spawn, despawn, pooling
│   └── EnemyAnimator.cs          — Animation controller
├── Weapons/
│   ├── WeaponBase.cs             — Base class vũ khí
│   ├── WeaponData.cs             — ScriptableObject data
│   ├── WeaponInventory.cs        — Quản lý inventory vũ khí
│   ├── Projectile.cs             — Đạn (nếu dùng projectile-based)
│   ├── WeaponEffects.cs          — Muzzle flash, shell eject, recoil
│   ├── GrenadeSystem.cs          — Ném lựu đạn, molotov
│   └── WeaponUpgrades.cs         — Crafting & upgrade
├── UI/
│   ├── UIManager.cs              — Quản lý tất cả UI
│   ├── HUDController.cs           — HUD trong game
│   ├── InventoryUI.cs            — Màn hình inventory
│   ├── MenuManager.cs            — Main menu, pause menu
│   ├── DialogSystem.cs           — Dialog NPC
│   ├── CrosshairUI.cs            — Crosshair, hit marker
│   ├── HealthBarUI.cs            — HP bar animation
│   ├── WaveUI.cs                 — Wave counter, wave start
│   └── DamageOverlay.cs          — Màn hình đỏ khi nhận damage
├── Managers/
│   ├── GameManager.cs            — Trạng thái game tổng thể
│   ├── WaveManager.cs            — Quản lý wave, spawn logic
│   ├── MissionManager.cs          — Quản lý nhiệm vụ, checkpoint
│   ├── SaveLoadManager.cs        — Lưu/tải game
│   ├── SceneTransitionManager.cs — Load scene, fade
│   ├── TimeOfDayManager.cs       — Cycle ngày/đêm
│   └── DifficultyManager.cs      — Scale difficulty
├── Audio/
│   ├── AudioManager.cs           — Quản lý tất cả âm thanh
│   ├── MusicSystem.cs            — Nhạc nền theo tình huống
│   ├── SFXManager.cs             — Hiệu ứng âm thanh
│   └── FootstepSystem.cs         — Bước chân theo bề mặt
├── Environment/
│   ├── LootSpawner.cs            — Spawn loot
│   ├── DoorController.cs         — Cửa mở/đóng
│   ├── ElevatorController.cs     — Thang máy
│   ├── BreakableObject.cs        — Vật thể phá hủy
│   └── TrapSystem.cs             — Bẫy (tùy map)
├── Narrative/
│   ├── JournalEntry.cs           — Thư, tài liệu người chơi nhặt được
│   ├── AudioLogPickup.cs         — Audio log pickup
│   ├── StoryTrigger.cs           — Trigger cutscene/dialog
│   └── EndingManager.cs          — Quản lý kết thúc
└── Common/
    ├── Singleton.cs              — Base singleton
    ├── ObjectPool.cs             — Object pooling system
    ├── EventBus.cs               — Event-driven communication
    ├── SettingsManager.cs        — Cài đặt (sensitivity, volume, etc.)
    └── Constants.cs              — Hằng số game
```

## 9.2 Object Pooling

Zombie và đạn được **pool** thay vì instantiate/destroy liên tục:

- **Zombie Pool:** 50 slot (có thể mở rộng). Khi zombie chết → trả về pool → reuse.
- **Bullet Pool:** 200 slot. Đạn bay ra → trả về pool sau 2s hoặc khi trúng target.
- **Loot Pool:** 30 slot. Item spawn → tồn tại 60s → despawn nếu không nhặt.

## 9.3 NavMesh cho AI

- Sử dụng **Unity NavMesh** cho pathfinding của zombie
- NavMesh baking cho mỗi khu vực (load additive scene)
- Zombie thường (Walker, Runner, Crawler) dùng NavMeshAgent
- Brute dùng **RVO** avoidance để tránh đâm vào zombie khác
- Crawler có thể tắt avoidance để bò qua chỗ hẹp

## 9.4 Performance Targets

| Metric | Mục tiêu |
|---|---|
| FPS | 60 FPS (average), 30 FPS minimum |
| Zombie đồng thời | 30 (tối đa) |
| Draw calls | < 2000 |
| Physics | Fixed timestep 60Hz |
| Load time | < 5s per scene |
| Memory | < 4GB RAM |

---

# PHẦN X — MONETIZATION & PHÂN PHỐI

## 10.1 Mô hình kinh doanh

**Giá đề xuất:** $14.99 (Early Access)

**Giai đoạn phát hành:**
- **Early Access (Tháng 1–3):** MVP + Act 1–2. Giá $9.99. Thu thập feedback.
- **Full Release (Tháng 6):** Toàn bộ game. Giá $14.99.
- **Launch Discount:** 20% off trong tuần đầu.

## 10.2 Nội dung mở rộng (DLC)

- **DLC 1 — "Silent Night":** Campaign nhỏ về sự kiện Ngày 0 từ góc nhìn Elena
- **DLC 2 — "The Lab":** Khám phá phòng thí nghiệm Helix dưới lòng đất, nhiều zombie thử nghiệm
- **Survival Mode** (miễn phí): Chế độ endless wave, leaderboard

---

# PHẦN XI — KẾ HOẠCH PHÁT TRIỂN

## Timeline

```
Tháng 1    Tháng 2    Tháng 3    Tháng 4    Tháng 5    Tháng 6
  │          │          │          │          │          │
  ├──────────┴──────────┴──────────┴──────────┴──────────┤
  │           GIAI ĐOẠN PHÁT TRIỂN                          │
  ├──────────┬──────────┬──────────┬──────────┬────────────┤
  │          │          │          │          │            │
  ▼          ▼          ▼          ▼          ▼            ▼
MVP        Alpha      Beta      Polish    Release     Post-launch
Build     Phase 1    Full      Content   Launch     Support
Prototype +Acts1-2   Content +  Bug fix    EA→Full   Community
Player               All Acts   Optimization          Feedback
Move +                + Audio/     + Audio
Shoot +               Visual      + Localization
Wave 1                Polish
```

### Milestone chi tiết

| Milestone | Nội dung | Tiêu chí đạt |
|---|---|---|
| **Prototype** | Player movement + 1 zombie + bắn súng | Có thể chơi được trong 5 phút |
| **MVP** | Wave system + đủ 4 loại zombie + 2 vũ khí + 1 map | Có thể chơi từ đầu đến cuối 1 mission |
| **Alpha 1** | Act 1–2 hoàn chỉnh, tất cả zombie, tất cả vũ khí, 3 map | 60% content hoàn thành |
| **Alpha 2** | Act 3–4 + kết thúc A/B/C + side quest | 85% content hoàn thành |
| **Beta** | Tất cả nội dung + audio + polish + optimization | Feature complete |
| **RC** | Bug fix + balance + localization | Release-ready |
| **Launch** | Early Access release | — |
| **Full Release** | Toàn bộ game | — |

---

# PHẦN XII — RỦI RO VÀ GIẢI PHÁP

| Rủi ro | Mức độ | Giải pháp |
|---|---|---|
| Zombie AI quá phức tạp | Cao | Bắt đầu với FSM đơn giản, thêm layer behavior từ từ. Đừng cố gắng làm "perfect AI" ngay. |
| Performance với nhiều zombie | Cao | Object pooling + LOD + culling sớm. Đặt cap 30 zombie đồng thời. |
| Scope creep | Trung | Dùng GDD như "hợp đồng". Cut feature nếu chậm tiến độ. Prioritize MVP. |
| Chưa có art asset | Trung | Prototype với primitive shapes (box, sphere, capsule). Thay bằng asset thật khi có budget. |
| Gameplay không fun | Trung | Playtest sớm và thường xuyên. Nếu không fun → fix gameplay trước, polish sau. |
| Thời gian phát triển kéo dài | Cao | Chia nhỏ milestone. Mỗi tuần review scope. Cắt bớt nếu cần. |

---

# PHẦN XIII — THAM KHẢO & CẢM HỨNG

## Game tham khảo

| Game | Yếu tố tham khảo |
|---|---|
| **Left 4 Dead 2** | Wave system, AI Director, đa dạng zombie, weapon feel |
| **The Last of Us** | Câu chuyện, nhân vật, environmental storytelling, UI tối giản |
| **Resident Evil 2 Remake** | Atmosphere, tension, resource management, map design |
| **Doom Eternal** | Weapon feel, movement, combat flow |
| **DayZ** | Survival elements, loot, crafting |

## Phim & TV tham khảo

| Phim/TV | Yếu tố tham khảo |
|---|---|
| **28 Days Later** | Atmosphere, "infected" không phải "zombie", im lặng |
| **The Last of Us (HBO)** | Tone câu chuyện, character-driven |
| **Dawn of the Dead (2004)** | Survival trong không gian quen thuộc, shopping mall |
| **Train to Busan** | Căng thẳng trong không gian hẹp, nhân vật |

## Âm nhạc tham khảo

| Game/Album | Phong cách |
|---|---|
| **The Last of Us — Gustavo Santaolalla** | Main theme, emotional piano |
| **Left 4 Dead 2 — In-house** | Combat music, situational |
| **DOOM 2016 — Mick Gordon** | Boss music, industrial |

---

# PHỤ LỤC — CHECKLIST PHÁT TRIỂN

## Phase 1 (MVP) — Checklist

- [ ] Player movement (WASD, jump, sprint, crouch)
- [ ] Camera FPS với mouse look
- [ ] Shooting system (M1911)
- [ ] Reloading system
- [ ] Hit detection (raycast)
- [ ] Zombie Walker với basic AI
- [ ] Wave system (spawn, wave count, wave end)
- [ ] HUD (HP bar, stamina, ammo, wave counter, crosshair)
- [ ] Loot system (spawn, pickup)
- [ ] 1 map demo (Warehouse / Old Town)
- [ ] Game Over state

## Phase 2 — Checklist

- [ ] Tất cả 5 loại zombie với đầy đủ AI
- [ ] Tất cả 7 vũ khí
- [ ] Health/Stamina system
- [ ] Grenade system
- [ ] Inventory system (weapon + item)
- [ ] Crafting system
- [ ] Weapon upgrade
- [ ] Side quest system
- [ ] 3 map đầu tiên (Old Town, Northside, Hospital)

## Phase 3 — Checklist

- [ ] Act 3–4 campaign + kết thúc A/B/C
- [ ] Tất cả 7 map
- [ ] Dialog system với NPC
- [ ] Audio log system
- [ ] Save/Load system
- [ ] Mini-map
- [ ] Boss fight (Bulwark)
- [ ] Full audio (SFX + Music)
- [ ] Full UI (all menus, inventory, dialog)
- [ ] Optimization & bug fix

---

*Tài liệu Phiên bản: 1.0*
*Ngày cập nhật: 03/05/2026*
*Tác giả: Game Design Team*
*Trạng thái: Sẵn sàng phát triển*
