# Blinker-Canceller
ウインカーキャンセラーカムの動作音を提供するOMSI 2車両向けスクリプト

## インストール方法
1. `Script System` フォルダと `sound` フォルダを、車両MODのルートフォルダにコピーします。（例: `OMSI 2\Vehicles\[Public]HINO_Rainbow`）
2. `*.bus` を以下のように編集します。
   
   ```ini
   [varnamelist]
   28  # ★ 元の値に1を足す
   # ... (省略)
   Script System\blinker_canceller\varlist.txt  # ★ 追加

   [script]
   31  # ★ 元の値に1を足す
   # ... (省略)
   Script System\lights\lights.osc
   Script System\blinker_canceller\main.osc  # ★ 追加
   Script System\door\b0\door_FE.osc
   # ... (省略)

   [constfile]
   28  # ★ 元の値に1を足す
   # ... (省略)
   Script System\blinker_canceller\constfile.txt  # ★ 追加
   ```

3. `Script System\main\main.osc` を以下のように編集します。

   ```osc
   {init}
       (M.L.engine_Init)
   '   ... (省略)
   '   ★ 追加
       (M.L.blinker_canceller_init)
   '   ... (省略)
   {end}

   {frame}
       (M.L.Engine_Frame)
   '   ... (省略)
   '   ★ 追加
       (M.L.blinker_canceller_frame)
   '   ... (省略)
   {end}
   ```

4. `sound\sound_*.cfg` を以下のように編集します。(例: `sound_J07E_5MT_Front_Entry.cfg`)

   ```ini
   # ... (省略)
   [sound]
   D89_blinker_swon.wav
   1
   # ... (省略)
   [trigger]
   ev_lights_blinker_swon

   # ★ 追加ここから
   [sound]
   blinker_canceller\bc_cam_snapped.wav
   3

   [3d]
   -0.82626
   5.01923
   1.35706
   0.5

   [viewpoint]
   2

   [trigger]
   ev_blinker_cam_position_changed
   # ★ 追加ここまで
   # ... (省略)
   ```
