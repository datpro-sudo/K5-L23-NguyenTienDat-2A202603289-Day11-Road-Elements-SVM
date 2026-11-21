# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Lê Minh Thắng (`2A202603292`) — task `24`, job `24`, task front A01–A06; tài khoản CVAT hiển thị `thang`.

Người kiểm (học viên): Nguyễn Tiến Đạt (`2A202603289`).

Ngày: 20/11/2026 (Asia/Bangkok) — Phiên bản guideline: Road v1.0.

File được kiểm (tên + `revision` trong manifest): chưa có file export/manifest; kiểm hiện trạng qua 14 ảnh chụp người dùng cung cấp.

Số ảnh kiểm: **6**, A01–A06 (+ **0** ảnh thêm). Số nhãn đã rà qua ảnh chụp (shape + tag): **45 = 21 shape + 24 tag**.

> Đây là phiếu QC qua ảnh chụp, chưa phải xác nhận hoàn tất QC trên file xuất. Các ảnh chụp cùng mã ảnh được gộp, không đếm lặp nhãn. Chỉ đưa phát hiện đủ căn cứ vào danh sách lỗi; các nội dung chưa xác minh nằm ở mục Ca mơ hồ. Không suy ra thứ tự điểm, độ lệch chính xác 5 px hoặc tính hợp lệ của file XML từ một ảnh chụp.

## Phạm vi và bằng chứng

| Ảnh | Ảnh chụp trong tin nhắn | Shape đã rà | Tag có mặt | Tổng nhãn |
| --- | --- | --- | ---: | ---: |
| A01 | #1–#3 | 4 lane: id 12, 17, 18, 19 | 4 | 8 |
| A02 | #4–#5 | 3 lane: id 25, 26, 27 | 4 | 7 |
| A03 | #6–#7 | 3 lane: id 33, 34, 35 | 4 | 7 |
| A04 | #8–#10 | 3 lane: id 40, 41, 42; 2 drivable: id 44, 45 | 4 | 9 |
| A05 | #11–#12 | 2 road_curb: id 50, 51; 1 drivable: id 108 | 4 | 7 |
| A06 | #13–#14 | 2 road_curb: id 52, 53; 1 lane: id 54 | 4 | 7 |
| **Tổng** | **14 ảnh chụp / 6 ảnh dữ liệu** | **14 lane + 4 road_curb + 3 drivable = 21 shape** | **24** | **45** |

- Đã đối chiếu thêm ảnh gốc A01–A06 trong `data/`, không sử dụng GT của coach.
- Cả 6 ảnh đều thấy đủ 4 tag; `camera=front`, `source=real`. A05 có `weather=overcast`; các ảnh còn lại đang chọn `clear`. Tính phù hợp của weather ở A03/A04 cần rà thêm như bảng Ca mơ hồ.
- A01: chưa ghi nhận lỗi chắc chắn trong phần quan sát được; các giá trị lane hiển thị phù hợp (L1/R1 trắng đứt đơn, L2 trắng liền đôi, R2 vàng liền đơn). Chưa xác nhận đạt ngưỡng hình học 5 px.
- Thiếu bảng kế hoạch label theo từng ảnh trong slide Task 1. Không tự quy lỗi thiếu đèn/biển chỉ vì nhìn thấy đèn/biển nhưng chưa có box; cần xác nhận chúng thuộc phạm vi bắt buộc của ảnh đó. A06 có trọng tâm vạch qua đường trong repo (`src/road_lab/select_bdd_road.py`), nên thiếu crosswalk được ghi nhận.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 tag camera | 0 phát hiện | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 ảnh | 0 xác nhận; A05/A06 chờ đối chiếu khả năng nhìn thấy vạch | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 lane | 0 xác nhận; A03/R2 chờ xác minh | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 lane, rà hình học bằng mắt | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 7 lane có style=dashed, rà cách nối | 0 tách vạch quan sát được; chưa xác minh đầy đủ occluded | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 lane | 1 nhãn sai thuộc tính | chính |
| QC1-07 vùng lái | sai thuộc tính / sai phạm vi / bỏ sót | 8 mục: 3 drivable + 4 road_curb + 1 crosswalk cần có | 3: 2 tạm xếp nặng + 1 chính | chính theo bảng mã; xem giải thích mức A04 bên dưới |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 0 box được kiểm | Chưa kết luận do thiếu bảng phạm vi từng ảnh | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 0 box được kiểm | Chưa kết luận | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 0 box được kiểm | Chưa kết luận do thiếu bảng phạm vi từng ảnh | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | Không áp dụng: cả 6 ảnh là front | chính |
| QC1-12 file | lỗi file | 0 file export được kiểm | Chưa kiểm; không coi việc chưa cung cấp export là lỗi file | nhẹ / nặng |

**Cách đếm:** số mục kiểm ở từng mã có thể trùng cùng một nhãn, không cộng các dòng để làm mẫu số. Mẫu số của đợt rà này là 45 nhãn hiện hữu ở bảng phạm vi. Nhãn crosswalk bị bỏ sót chưa tồn tại nên không cộng vào 45. Cùng một nhãn sai cả color và kind được ghi gộp thành một phát hiện QC1-06; hai polygon A04 là hai nhãn khác nhau nên ghi hai dòng, không đếm lại lỗi đảo vùng ở mã khác.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A02 | lane, id 27, L2 | chính | Điểm gần xe dừng ở vệt sơn phía trong ảnh; vẫn còn một vệt trắng của cùng vạch ở mép trái, thấp hơn (thấy ở ảnh chụp #4/#5 và ảnh gốc). Cần nối cùng polyline tới phần gần nhất còn thấy ở mép ảnh, không bỏ vệt gần này. |
| 2 | QC1-06 | A03 | lane, id 33, L1 | chính | Details đang là solid / white / single. Vệt sơn được vẽ là màu vàng, đoạn gần xe thấy hai nét song song. Sửa color=yellow, kind=double; giữ solid. Nếu coach xác định hai nét thuộc cấu trúc vạch hỗn hợp thì chốt kind theo ca mơ hồ bên dưới, nhưng sai color=white là phát hiện chắc chắn. |
| 3 | QC1-07 | A04 | drivable, id 44 | nặng, tạm xếp theo tiêu chí nhầm làn | Polygon nằm bên phải vạch trắng đứt R1, giữa R1 và cặp vạch trắng bên phải, nhưng area_type=direct. Xe mình đang ở làn bên trái R1, giữa vạch vàng đôi và R1. Đổi polygon này thành alternative. Bằng chứng: vùng tô xanh ở ảnh chụp #10. |
| 4 | QC1-07 | A04 | drivable, id 45 | nặng, tạm xếp theo tiêu chí nhầm làn | Polygon làn mình đi (giữa vàng đôi L1 và trắng đứt R1) đang mang area_type=alternative. Đổi thành direct. Đây là nửa còn lại của lỗi đảo hai vùng ở A04, chỉ tính một lần cho polygon id 45. |
| 5 | QC1-07 | A06 | crosswalk, chưa có id | chính | Vùng vạch qua đường ngang phía trước nhìn thấy rõ nhưng chưa có polygon crosswalk. Cả hai ảnh chụp #13/#14 đều có Items=7, khớp đúng 4 tag + 2 road_curb + 1 lane, không có crosswalk. Tạo một polygon bao cả vùng các vạch, không tách mỗi vệt thành một shape; không kéo polygon vào vỉa hè hoặc phần sau cột. |

**Lưu ý xếp mức cho A04:** mục 1 của `docs/qc_severity_road_v1.0.md` nêu “nhầm làn của mình với làn bên cạnh” là lỗi nặng, trong khi bảng ở mục 2 ghi QC1-07 là chính. Phiếu áp dụng chỉ dẫn của tài liệu: khi phân vân chọn mức cao hơn và hỏi lead. Vì vậy hai nhãn đảo area_type tạm xếp nặng, cần lead xác nhận mức cuối. Nếu chuyển cả hai sang chính thì kết luận vẫn là Rework do 5/45 = 11,11% > 5%.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A04 | Hai polygon id 44/45 đảo direct/alternative: áp dụng mức nặng theo ví dụ mục 1 hay chính theo bảng mã QC1-07 mục 2? | Chưa có lời đáp. Tạm xếp nặng; dù hạ cả hai xuống chính vẫn Rework. |
| A03 | L1/id 33: đoạn gần thấy hai nét vàng, phía xa nhập vào vùng gạch chéo. Xác nhận kind=double và cách đại diện đoạn chuyển tiếp. | Chưa có lời đáp. Cần sửa color=yellow trước; không đếm thêm lỗi thứ hai cho cùng nhãn ở QC1-06. |
| A03 | R1/id 34: đường vẽ và đầu gần có dấu hiệu lệch tâm vệt trắng quanh chữ SCHOOL. Cần mở ở tỉ lệ ảnh gốc để đo; R2/id 35 có thực là vạch sơn hay đường suy diễn theo hàng xe đỗ? | Chưa đủ căn cứ đo 5 px/xác nhận đối tượng. Chưa cộng lỗi QC1-04 hoặc QC1-03 cho các nghi vấn này. |
| A03 | Checkpoint yêu cầu có occluded; đã bật đúng trên đoạn bị che nào? | R2 hiển thị nét đứt có thể là cách CVAT biểu diễn occluded; không đồng nhất nét đứt hiển thị với thuộc tính style=dashed. Cần xem trạng thái cờ và vị trí bị che, chưa kết luận thiếu occluded. |
| A03, A04 | Weather đang là clear; trời nhiều mây trong ảnh gốc. Chọn clear (ít mây) hay overcast (âm u, nhiều mây)? A03 có cần dusk thay day? | Chờ đối chiếu nguồn/coach, không suy ra dusk chỉ từ màu ấm của tòa nhà. Chưa tính lỗi tag do quy tắc mức cho tag môi trường sai giá trị chưa được bảng mã nêu rõ. |
| A05 | Drivable/id 108 uốn theo từng xe đỗ. Biên có lấn vào các khoảng trống thuộc dải đỗ hay chỉ đang loại đúng dải đỗ sát lề? | Cần coach xác nhận biên chức năng của dải đỗ. Không yêu cầu phủ toàn bộ phần dưới xe đỗ: guideline loại dải đỗ khỏi direct. Biên phải theo làn đang đi, không bám hình từng xe hoặc mở vào khe đỗ. Chưa cộng lỗi. |
| A05, A06 | Road_curb id 50/51 và 52/53: có đoạn chạy qua hình chiếu xe/cột; đã theo đúng mép đường hay bám hàng xe? Có đủ căn cứ nối qua phần bị che? | Cần rà lại phần curb còn thấy và hướng nối; chưa có GT hoặc phép đo để chốt sai phạm vi. Không coi đường nối qua vật che tự nó là lỗi. |
| A05, A06 | A05 không có lane; A06 chỉ có L1/id 54. Có nhìn thấy vạch R1 thực sự để bắt buộc gán không? | Không tự tạo lane theo lề/xe đỗ và không kết luận lỗi nặng chỉ từ thiếu L1/R1 trong danh sách. Nếu không thấy vạch, nhờ coach xác nhận ngoại lệ QC1-02 và ghi lý do theo CHECKPOINTS. |
| A01–A06 | Bảng slide Task 1 yêu cầu những nhóm nhãn nào ở mỗi ảnh? Đặc biệt A03/A04/A06 có bắt buộc box đèn/biển không? | Repo chưa kèm bảng slide, manifest_front.csv chỉ có tiêu đề. Chưa quy lỗi thiếu box; nếu thuộc phạm vi thì rà mọi đèn/biển cao từ 8 px ở ảnh gốc. |
| A01–A06 | Chiều điểm gần → xa, lệch tâm tối đa 5 px, cờ occluded và file xuất có đúng không? | Chưa có XML/zip/manifest. Không chứng nhận đạt các kiểm tra này qua ảnh chụp. Cần xem thứ tự điểm, thuộc tính gốc và chạy lint sau export. |

## Quyết định
Lỗi nặng: **2, tạm xếp mức, chờ lead xác nhận**. Lỗi chính: **3 / 45 nhãn = 6,67%**. Lỗi nhẹ: **0 đã xác nhận**. Ca chờ lead/xác minh bổ sung: **10 dòng** ở bảng trên.

Quyết định (Release / Hold / Rework): **Rework — cho phần mẫu A01–A06 đã rà qua ảnh chụp**.

Lý do (theo luật của phiếu): **3 lỗi chính đã đủ vượt 5%**, kể cả chưa xét hai lỗi A04 đang tạm xếp nặng. Có lỗi phải sửa đã xác nhận nên không dùng Hold để thay thế Rework; các ca mơ hồ cần chốt khi kiểm lại. Nếu lead hạ hai lỗi A04 xuống chính, số lỗi chính là **5 / 45 = 11,11%**, vẫn Rework. Chưa kết luận chất lượng toàn bộ task front, phần fisheye hoặc file bàn giao.

## Việc cần sửa và kiểm lại

1. A02: kéo dài L2/id 27 tới vệt gần nhất còn thấy ở mép trái, giữ một polyline.
2. A03: sửa L1/id 33 sang yellow; rà kind=double và hình học R1, xác minh R2/occluded.
3. A04: đổi id 45 thành direct, id 44 thành alternative. Giữ vùng direct ở làn mình đi; không đưa vùng làn xe đạp sát vỉa vào hai polygon.
4. A05: rà biên direct theo dải đỗ và các đoạn road_curb; không sửa vùng lái theo quy tắc phủ xe khi đó là dải đỗ bị loại khỏi direct.
5. A06: thêm polygon crosswalk bao toàn bộ vùng vạch qua đường; rà phần bị che bởi xe/cột và không tràn lên vỉa hè.
6. Chốt bảng phạm vi label, các ca mơ hồ; kiểm ở ảnh gốc, rồi kiểm file export/manifest trước khi ghi nhận đã sửa và quyết định lại.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
