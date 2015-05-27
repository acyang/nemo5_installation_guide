# 5.結果測試

編譯成功後，到NEMO5_HOEM/regression_test/numerical_tests資料夾選定一個CASE做測試。

```
cd Cu_wire_readin_test
/PATH/TO/NEMO5/EXEC Cu_wire_1x1uc.in > test.log
```

Cu_wire_1x1uc.in需要修改檔案最後的materialdatabase路徑。

```
/ ########################################################################################################
// define solvers in the Global section
Global
{
  solve = (new_Repartition_device,device_concat,draw_new_device++,&
          source_source_source_concat,source_source_concat,source_concat,&
          drain_drain_drain_concat,drain_drain_concat,drain_concat,&
          draw_drain++,draw_drain_drain++,draw_drain_drain_drain++,&
          draw_source++,draw_source_source++,draw_source_source_source++,d1++)

  output = (new_Repartition_device,d1:QTBM_test2)
  database = /pkg/biology/Nemo5/Nemo5_r17881/prototype/materials/all.mat
  message_level = 5
}
```

test.log仔細確認有無error發生

```
===============================================
Welcome to NEMO 5
Compiled on Apr 29 2015 at 09:32:28
Hostname: alpi4
Compiled with: g++ (SUSE Linux) 4.8.3
SVN revision: exported

Current time: Wed Apr 29 12:17:03 2015
Time zone: CST
Master process: alpi4
===============================================
===========================================================
[Nemo] Parsing NEMO5 inputdeck...
===========================================================
[Nemo] parsing input file Cu_wire_1x1uc.in...
[Nemo] NEW database parsed okay
[Nemo] finished reading input deck after 0.066885 s.
[Nemo/PetscMatrixDouble] Initializing DOUBLE SLEPc...
[Nemo/PetscMatrixComplex] Initializing COMPLEX SLEPc...
Running NEMO on 1 nodes.
===========================================================
[Nemo] initializing Material regions...
===========================================================
[Material] creating Cu...
  [Crystal] initializing...
[Nemo] Material regions were initialized in 0.000715971 seconds.
[SimpleShapes] creating shapes...
[SimpleShapes] shape creation is done.
[SimpleShapes] creating shapes...
[SimpleShapes] shape creation is done.
[Nemo] Geometry was initialized in 0.000386 seconds.
===========================================================
[Nemo] initializing Domains...
===========================================================
read atom position file
[test new code]: generate_NEMO5_coupling_file. 
Finish reading position and translation vectors.
Get translation of xy plain.  Size 240
Get translation of -z plain. 
Get translation of z plain. 
after translation, total coordinates is 720 720
Cu-Cu=0.362
atom # 0
atom # 1
atom # 2
atom # 3
atom # 4
atom # 5
atom # 6
atom # 7
atom # 8
atom # 9
atom # 10
atom # 11
atom # 12
atom # 13
atom # 14
atom # 15
atom # 16
atom # 17
atom # 18
atom # 19
atom # 20
atom # 21
atom # 22
atom # 23
atom # 24
atom # 25
atom # 26
atom # 27
atom # 28
atom # 29
atom # 30
atom # 31
atom # 32
atom # 33
atom # 34
atom # 35
atom # 36
atom # 37
atom # 38
atom # 39
atom # 40
atom # 41
atom # 42
atom # 43
atom # 44
atom # 45
atom # 46
atom # 47
atom # 48
atom # 49
atom # 50
atom # 51
atom # 52
atom # 53
atom # 54
atom # 55
atom # 56
atom # 57
atom # 58
atom # 59
atom # 60
atom # 61
atom # 62
atom # 63
atom # 64
atom # 65
atom # 66
atom # 67
atom # 68
atom # 69
atom # 70
atom # 71
atom # 72
atom # 73
atom # 74
atom # 75
atom # 76
atom # 77
atom # 78
atom # 79
atom # 80
atom # 81
atom # 82
atom # 83
atom # 84
atom # 85
atom # 86
atom # 87
atom # 88
atom # 89
atom # 90
atom # 91
atom # 92
atom # 93
atom # 94
atom # 95
atom # 96
atom # 97
atom # 98
atom # 99
atom # 100
atom # 101
atom # 102
atom # 103
atom # 104
atom # 105
atom # 106
atom # 107
atom # 108
atom # 109
atom # 110
atom # 111
atom # 112
atom # 113
atom # 114
atom # 115
atom # 116
atom # 117
atom # 118
atom # 119
atom # 120
atom # 121
atom # 122
atom # 123
atom # 124
atom # 125
atom # 126
atom # 127
atom # 128
atom # 129
atom # 130
atom # 131
atom # 132
atom # 133
atom # 134
atom # 135
atom # 136
atom # 137
atom # 138
atom # 139
atom # 140
atom # 141
atom # 142
atom # 143
atom # 144
atom # 145
atom # 146
atom # 147
atom # 148
atom # 149
atom # 150
atom # 151
atom # 152
atom # 153
atom # 154
atom # 155
atom # 156
atom # 157
atom # 158
atom # 159
atom # 160
atom # 161
atom # 162
atom # 163
atom # 164
atom # 165
atom # 166
atom # 167
atom # 168
atom # 169
atom # 170
atom # 171
atom # 172
atom # 173
atom # 174
atom # 175
atom # 176
atom # 177
atom # 178
atom # 179
atom # 180
atom # 181
atom # 182
atom # 183
atom # 184
atom # 185
atom # 186
atom # 187
atom # 188
atom # 189
atom # 190
atom # 191
atom # 192
atom # 193
atom # 194
atom # 195
atom # 196
atom # 197
atom # 198
atom # 199
atom # 200
atom # 201
atom # 202
atom # 203
atom # 204
atom # 205
atom # 206
atom # 207
atom # 208
atom # 209
atom # 210
atom # 211
atom # 212
atom # 213
atom # 214
atom # 215
atom # 216
atom # 217
atom # 218
atom # 219
atom # 220
atom # 221
atom # 222
atom # 223
atom # 224
atom # 225
atom # 226
atom # 227
atom # 228
atom # 229
atom # 230
atom # 231
atom # 232
atom # 233
atom # 234
atom # 235
atom # 236
atom # 237
atom # 238
atom # 239
[InputStructure] Reading in atom file for translation vectors  
6	0	0
0	6	0
0	0	30
[Nemo] Domains were initialized in 0.197726 seconds.
[InputStructure] Reading in atom file 
Atom id: 0 atomtype: Cu Region: 1
Atom id: 1 atomtype: Cu Region: 1
Atom id: 2 atomtype: Cu Region: 1
Atom id: 3 atomtype: Cu Region: 1
Atom id: 4 atomtype: Cu Region: 1
Atom id: 5 atomtype: Cu Region: 1
Atom id: 6 atomtype: Cu Region: 1
Atom id: 7 atomtype: Cu Region: 1
Atom id: 8 atomtype: Cu Region: 1
Atom id: 9 atomtype: Cu Region: 1
Atom id: 10 atomtype: Cu Region: 1
Atom id: 11 atomtype: Cu Region: 1
Atom id: 12 atomtype: Cu Region: 1
Atom id: 13 atomtype: Cu Region: 1
Atom id: 14 atomtype: Cu Region: 1
Atom id: 15 atomtype: Cu Region: 1
Atom id: 16 atomtype: Cu Region: 1
Atom id: 17 atomtype: Cu Region: 1
Atom id: 18 atomtype: Cu Region: 1
Atom id: 19 atomtype: Cu Region: 1
Atom id: 20 atomtype: Cu Region: 1
Atom id: 21 atomtype: Cu Region: 1
Atom id: 22 atomtype: Cu Region: 1
Atom id: 23 atomtype: Cu Region: 1
Atom id: 24 atomtype: Cu Region: 1
Atom id: 25 atomtype: Cu Region: 1
Atom id: 26 atomtype: Cu Region: 1
Atom id: 27 atomtype: Cu Region: 1
Atom id: 28 atomtype: Cu Region: 1
Atom id: 29 atomtype: Cu Region: 1
Atom id: 30 atomtype: Cu Region: 1
Atom id: 31 atomtype: Cu Region: 1
Atom id: 32 atomtype: Cu Region: 1
Atom id: 33 atomtype: Cu Region: 1
Atom id: 34 atomtype: Cu Region: 1
Atom id: 35 atomtype: Cu Region: 1
Atom id: 36 atomtype: Cu Region: 1
Atom id: 37 atomtype: Cu Region: 1
Atom id: 38 atomtype: Cu Region: 1
Atom id: 39 atomtype: Cu Region: 1
Atom id: 40 atomtype: Cu Region: 1
Atom id: 41 atomtype: Cu Region: 1
Atom id: 42 atomtype: Cu Region: 1
Atom id: 43 atomtype: Cu Region: 1
Atom id: 44 atomtype: Cu Region: 1
Atom id: 45 atomtype: Cu Region: 1
Atom id: 46 atomtype: Cu Region: 1
Atom id: 47 atomtype: Cu Region: 1
Atom id: 48 atomtype: Cu Region: 1
Atom id: 49 atomtype: Cu Region: 1
Atom id: 50 atomtype: Cu Region: 1
Atom id: 51 atomtype: Cu Region: 1
Atom id: 52 atomtype: Cu Region: 1
Atom id: 53 atomtype: Cu Region: 1
Atom id: 54 atomtype: Cu Region: 1
Atom id: 55 atomtype: Cu Region: 1
Atom id: 56 atomtype: Cu Region: 1
Atom id: 57 atomtype: Cu Region: 1
Atom id: 58 atomtype: Cu Region: 1
Atom id: 59 atomtype: Cu Region: 1
Atom id: 60 atomtype: Cu Region: 1
Atom id: 61 atomtype: Cu Region: 1
Atom id: 62 atomtype: Cu Region: 1
Atom id: 63 atomtype: Cu Region: 1
Atom id: 64 atomtype: Cu Region: 1
Atom id: 65 atomtype: Cu Region: 1
Atom id: 66 atomtype: Cu Region: 1
Atom id: 67 atomtype: Cu Region: 1
Atom id: 68 atomtype: Cu Region: 1
Atom id: 69 atomtype: Cu Region: 1
Atom id: 70 atomtype: Cu Region: 1
Atom id: 71 atomtype: Cu Region: 1
Atom id: 72 atomtype: Cu Region: 1
Atom id: 73 atomtype: Cu Region: 1
Atom id: 74 atomtype: Cu Region: 1
Atom id: 75 atomtype: Cu Region: 1
Atom id: 76 atomtype: Cu Region: 1
Atom id: 77 atomtype: Cu Region: 1
Atom id: 78 atomtype: Cu Region: 1
Atom id: 79 atomtype: Cu Region: 1
Atom id: 80 atomtype: Cu Region: 1
Atom id: 81 atomtype: Cu Region: 1
Atom id: 82 atomtype: Cu Region: 1
Atom id: 83 atomtype: Cu Region: 1
Atom id: 84 atomtype: Cu Region: 1
Atom id: 85 atomtype: Cu Region: 1
Atom id: 86 atomtype: Cu Region: 1
Atom id: 87 atomtype: Cu Region: 1
Atom id: 88 atomtype: Cu Region: 1
Atom id: 89 atomtype: Cu Region: 1
Atom id: 90 atomtype: Cu Region: 1
Atom id: 91 atomtype: Cu Region: 1
Atom id: 92 atomtype: Cu Region: 1
Atom id: 93 atomtype: Cu Region: 1
Atom id: 94 atomtype: Cu Region: 1
Atom id: 95 atomtype: Cu Region: 1
Atom id: 96 atomtype: Cu Region: 1
Atom id: 97 atomtype: Cu Region: 1
Atom id: 98 atomtype: Cu Region: 1
Atom id: 99 atomtype: Cu Region: 1
Atom id: 100 atomtype: Cu Region: 1
Atom id: 101 atomtype: Cu Region: 1
Atom id: 102 atomtype: Cu Region: 1
Atom id: 103 atomtype: Cu Region: 1
Atom id: 104 atomtype: Cu Region: 1
Atom id: 105 atomtype: Cu Region: 1
Atom id: 106 atomtype: Cu Region: 1
Atom id: 107 atomtype: Cu Region: 1
Atom id: 108 atomtype: Cu Region: 1
Atom id: 109 atomtype: Cu Region: 1
Atom id: 110 atomtype: Cu Region: 1
Atom id: 111 atomtype: Cu Region: 1
Atom id: 112 atomtype: Cu Region: 1
Atom id: 113 atomtype: Cu Region: 1
Atom id: 114 atomtype: Cu Region: 1
Atom id: 115 atomtype: Cu Region: 1
Atom id: 116 atomtype: Cu Region: 1
Atom id: 117 atomtype: Cu Region: 1
Atom id: 118 atomtype: Cu Region: 1
Atom id: 119 atomtype: Cu Region: 1
Atom id: 120 atomtype: Cu Region: 1
Atom id: 121 atomtype: Cu Region: 1
Atom id: 122 atomtype: Cu Region: 1
Atom id: 123 atomtype: Cu Region: 1
Atom id: 124 atomtype: Cu Region: 1
Atom id: 125 atomtype: Cu Region: 1
Atom id: 126 atomtype: Cu Region: 1
Atom id: 127 atomtype: Cu Region: 1
Atom id: 128 atomtype: Cu Region: 1
Atom id: 129 atomtype: Cu Region: 1
Atom id: 130 atomtype: Cu Region: 1
Atom id: 131 atomtype: Cu Region: 1
Atom id: 132 atomtype: Cu Region: 1
Atom id: 133 atomtype: Cu Region: 1
Atom id: 134 atomtype: Cu Region: 1
Atom id: 135 atomtype: Cu Region: 1
Atom id: 136 atomtype: Cu Region: 1
Atom id: 137 atomtype: Cu Region: 1
Atom id: 138 atomtype: Cu Region: 1
Atom id: 139 atomtype: Cu Region: 1
Atom id: 140 atomtype: Cu Region: 1
Atom id: 141 atomtype: Cu Region: 1
Atom id: 142 atomtype: Cu Region: 1
Atom id: 143 atomtype: Cu Region: 1
Atom id: 144 atomtype: Cu Region: 1
Atom id: 145 atomtype: Cu Region: 1
Atom id: 146 atomtype: Cu Region: 1
Atom id: 147 atomtype: Cu Region: 1
Atom id: 148 atomtype: Cu Region: 1
Atom id: 149 atomtype: Cu Region: 1
Atom id: 150 atomtype: Cu Region: 1
Atom id: 151 atomtype: Cu Region: 1
Atom id: 152 atomtype: Cu Region: 1
Atom id: 153 atomtype: Cu Region: 1
Atom id: 154 atomtype: Cu Region: 1
Atom id: 155 atomtype: Cu Region: 1
Atom id: 156 atomtype: Cu Region: 1
Atom id: 157 atomtype: Cu Region: 1
Atom id: 158 atomtype: Cu Region: 1
Atom id: 159 atomtype: Cu Region: 1
Atom id: 160 atomtype: Cu Region: 1
Atom id: 161 atomtype: Cu Region: 1
Atom id: 162 atomtype: Cu Region: 1
Atom id: 163 atomtype: Cu Region: 1
Atom id: 164 atomtype: Cu Region: 1
Atom id: 165 atomtype: Cu Region: 1
Atom id: 166 atomtype: Cu Region: 1
Atom id: 167 atomtype: Cu Region: 1
Atom id: 168 atomtype: Cu Region: 1
Atom id: 169 atomtype: Cu Region: 1
Atom id: 170 atomtype: Cu Region: 1
Atom id: 171 atomtype: Cu Region: 1
Atom id: 172 atomtype: Cu Region: 1
Atom id: 173 atomtype: Cu Region: 1
Atom id: 174 atomtype: Cu Region: 1
Atom id: 175 atomtype: Cu Region: 1
Atom id: 176 atomtype: Cu Region: 1
Atom id: 177 atomtype: Cu Region: 1
Atom id: 178 atomtype: Cu Region: 1
Atom id: 179 atomtype: Cu Region: 1
Atom id: 180 atomtype: Cu Region: 1
Atom id: 181 atomtype: Cu Region: 1
Atom id: 182 atomtype: Cu Region: 1
Atom id: 183 atomtype: Cu Region: 1
Atom id: 184 atomtype: Cu Region: 1
Atom id: 185 atomtype: Cu Region: 1
Atom id: 186 atomtype: Cu Region: 1
Atom id: 187 atomtype: Cu Region: 1
Atom id: 188 atomtype: Cu Region: 1
Atom id: 189 atomtype: Cu Region: 1
Atom id: 190 atomtype: Cu Region: 1
Atom id: 191 atomtype: Cu Region: 1
Atom id: 192 atomtype: Cu Region: 1
Atom id: 193 atomtype: Cu Region: 1
Atom id: 194 atomtype: Cu Region: 1
Atom id: 195 atomtype: Cu Region: 1
Atom id: 196 atomtype: Cu Region: 1
Atom id: 197 atomtype: Cu Region: 1
Atom id: 198 atomtype: Cu Region: 1
Atom id: 199 atomtype: Cu Region: 1
Atom id: 200 atomtype: Cu Region: 1
Atom id: 201 atomtype: Cu Region: 1
Atom id: 202 atomtype: Cu Region: 1
Atom id: 203 atomtype: Cu Region: 1
Atom id: 204 atomtype: Cu Region: 1
Atom id: 205 atomtype: Cu Region: 1
Atom id: 206 atomtype: Cu Region: 1
Atom id: 207 atomtype: Cu Region: 1
Atom id: 208 atomtype: Cu Region: 1
Atom id: 209 atomtype: Cu Region: 1
Atom id: 210 atomtype: Cu Region: 1
Atom id: 211 atomtype: Cu Region: 1
Atom id: 212 atomtype: Cu Region: 1
Atom id: 213 atomtype: Cu Region: 1
Atom id: 214 atomtype: Cu Region: 1
Atom id: 215 atomtype: Cu Region: 1
Atom id: 216 atomtype: Cu Region: 1
Atom id: 217 atomtype: Cu Region: 1
Atom id: 218 atomtype: Cu Region: 1
Atom id: 219 atomtype: Cu Region: 1
Atom id: 220 atomtype: Cu Region: 1
Atom id: 221 atomtype: Cu Region: 1
Atom id: 222 atomtype: Cu Region: 1
Atom id: 223 atomtype: Cu Region: 1
Atom id: 224 atomtype: Cu Region: 1
Atom id: 225 atomtype: Cu Region: 1
Atom id: 226 atomtype: Cu Region: 1
Atom id: 227 atomtype: Cu Region: 1
Atom id: 228 atomtype: Cu Region: 1
Atom id: 229 atomtype: Cu Region: 1
Atom id: 230 atomtype: Cu Region: 1
Atom id: 231 atomtype: Cu Region: 1
Atom id: 232 atomtype: Cu Region: 1
Atom id: 233 atomtype: Cu Region: 1
Atom id: 234 atomtype: Cu Region: 1
Atom id: 235 atomtype: Cu Region: 1
Atom id: 236 atomtype: Cu Region: 1
Atom id: 237 atomtype: Cu Region: 1
Atom id: 238 atomtype: Cu Region: 1
Atom id: 239 atomtype: Cu Region: 1
Structure size240
Domain size240
Non local Domain size0
[Nemo] Domain coupling was initialized in 0.0154381 seconds.
option 1 set
option 1 complete
option 2 set
[Nemo] Domain was output in 0.0245011 seconds.
[Nemo] Material regions and Domains were initialized in 0.238799 seconds.
===========================================================
[Nemo] creating Simulations...
===========================================================
[Nemo] Simulation "new_Repartition_device" of type "Repartition" has been created.

[Nemo] Simulation "source_source_source_concat" of type "ConcatenateDomains" has been created.

[Nemo] Simulation "source_source_concat" of type "ConcatenateDomains" has been created.

[Nemo] Simulation "source_concat" of type "ConcatenateDomains" has been created.

[Nemo] Simulation "drain_drain_drain_concat" of type "ConcatenateDomains" has been created.

[Nemo] Simulation "drain_drain_concat" of type "ConcatenateDomains" has been created.

[Nemo] Simulation "drain_concat" of type "ConcatenateDomains" has been created.

[Nemo] Simulation "device_concat" of type "ConcatenateDomains" has been created.

[Nemo] Simulation "draw_new_device" of type "Structure" has been created.

[Nemo] Simulation "draw_source" of type "Structure" has been created.

[Nemo] Simulation "draw_source_source" of type "Structure" has been created.

[Nemo] Simulation "draw_source_source_source" of type "Structure" has been created.

[Nemo] Simulation "draw_drain" of type "Structure" has been created.

[Nemo] Simulation "draw_drain_drain" of type "Structure" has been created.

[Nemo] Simulation "draw_drain_drain_drain" of type "Structure" has been created.

[Nemo] Simulation "d1" of type "Dummy1" has been created.

[Nemo] Simulation "d1:schroed1" of type "Schroedinger_intra_atomic" has been created.

[Nemo] Simulation "d1:schroeds" of type "Schroedinger_intra_atomic" has been created.

[Nemo] Simulation "d1:schroedd" of type "Schroedinger_intra_atomic" has been created.

[Nemo] Simulation "d1:schroeddd" of type "Schroedinger_intra_atomic" has been created.

[Nemo] Simulation "d1:schroedss" of type "Schroedinger_intra_atomic" has been created.

no options!
[Nemo] Simulation "d1:Propagation_Parallelizer" of type "Green_Propagation" has been created.

[Nemo] Simulation "d1:source_Self_energy" of type "RetardedSelfModule" has been created.

[Nemo] Simulation "d1:drain_Self_energy" of type "RetardedSelfModule" has been created.

no options!
[Nemo] Simulation "d1:QTBM_test2" of type "QTBM_Propagation" has been created.

===========================================================
[Nemo] initializing Simulations...
===========================================================
NEMO tree new_Repartition_device
NEMO tree source_source_source_concat
NEMO tree source_source_concat
NEMO tree source_concat
NEMO tree drain_drain_drain_concat
NEMO tree drain_drain_concat
NEMO tree drain_concat
NEMO tree device_concat
NEMO tree draw_new_device
NEMO tree draw_source
NEMO tree draw_source_source
NEMO tree draw_source_source_source
NEMO tree draw_drain
NEMO tree draw_drain_drain
NEMO tree draw_drain_drain_drain
NEMO tree d1
NEMO tree d1:schroed1
NEMO tree d1:schroeds
NEMO tree d1:schroedd
NEMO tree d1:schroeddd
NEMO tree d1:schroedss
NEMO tree d1:Propagation_Parallelizer
NEMO tree d1:source_Self_energy
NEMO tree d1:drain_Self_energy
NEMO tree d1:QTBM_test2
    [Simulation] initializing material properties...  done.
    [Simulation] initializing boundary conditions...  boundary conditions are initialized.
[Schroedinger("d1:schroed1")] initializing...
[Schroedinger("d1:schroed1")] creating k-space object
[Schroedinger("d1:schroed1")] parallelizing...
[Schroedinger("d1:schroeds")] initializing...
[Schroedinger("d1:schroeds")] creating k-space object
[Schroedinger("d1:schroeds")] parallelizing...
[Schroedinger("d1:schroedd")] initializing...
[Schroedinger("d1:schroedd")] creating k-space object
[Schroedinger("d1:schroedd")] parallelizing...
[Schroedinger("d1:schroeddd")] initializing...
[Schroedinger("d1:schroeddd")] creating k-space object
[Schroedinger("d1:schroeddd")] parallelizing...
[Schroedinger("d1:schroedss")] initializing...
[Schroedinger("d1:schroedss")] creating k-space object
[Schroedinger("d1:schroedss")] parallelizing...
Simulation("draw_new_device")::set_simulation_domain("Domain_device_concat")
    [Simulation] initializing material properties...  done.
Simulation("draw_drain")::set_simulation_domain("Domain_drain_concat")
    [Simulation] initializing material properties...  done.
Simulation("draw_drain_drain")::set_simulation_domain("Domain_drain_drain_concat")
    [Simulation] initializing material properties...  done.
Simulation("draw_drain_drain_drain")::set_simulation_domain("Domain_drain_drain_drain_concat")
    [Simulation] initializing material properties...  done.
Simulation("draw_source")::set_simulation_domain("Domain_source_concat")
    [Simulation] initializing material properties...  done.
Simulation("draw_source_source")::set_simulation_domain("Domain_source_source_concat")
    [Simulation] initializing material properties...  done.
Simulation("draw_source_source_source")::set_simulation_domain("Domain_source_source_source_concat")
    [Simulation] initializing material properties...  done.
Simulation("d1:source_Self_energy")::set_simulation_domain("Domain_source_concat")
    [Simulation] initializing material properties...  done.
Simulation("d1")::trigger_command: (2) _step was send to Simulation d1:drain_Self_energy.
Simulation("d1:drain_Self_energy")::reinit()
Simulation("d1:drain_Self_energy")::set_simulation_domain("Domain_drain_concat")
    [Simulation] initializing material properties...  done.
Simulation("d1")::trigger_command: (3) _step was send to Simulation d1:schroed1.
Simulation("d1:schroed1")::reinit()
Simulation("d1:schroed1")::set_simulation_domain("Domain_device_concat")
    [Simulation] initializing material properties... New Intra Atomic Hamilton Constructor created

      [TBIntraAtomicHamiltonConstructor] initializing Cu...  done.
[Schroedinger("d1:schroed1")] re-initializing...
Simulation("d1:schroeds")::set_simulation_domain("Domain_source_concat")
    [Simulation] initializing material properties... New Intra Atomic Hamilton Constructor created

      [TBIntraAtomicHamiltonConstructor] initializing Cu...  done.
[Schroedinger("d1:schroeds")] re-initializing...
Simulation("d1:schroedd")::set_simulation_domain("Domain_drain_concat")
    [Simulation] initializing material properties... New Intra Atomic Hamilton Constructor created

      [TBIntraAtomicHamiltonConstructor] initializing Cu...  done.
[Schroedinger("d1:schroedd")] re-initializing...
Simulation("d1:schroeddd")::set_simulation_domain("Domain_drain_drain_concat")
    [Simulation] initializing material properties... New Intra Atomic Hamilton Constructor created

      [TBIntraAtomicHamiltonConstructor] initializing Cu...  done.
[Schroedinger("d1:schroeddd")] re-initializing...
Simulation("d1:schroedss")::set_simulation_domain("Domain_source_source_concat")
    [Simulation] initializing material properties... New Intra Atomic Hamilton Constructor created

      [TBIntraAtomicHamiltonConstructor] initializing Cu...  done.
[Schroedinger("d1:schroedss")] re-initializing...
Simulation("d1:QTBM_test2")::set_simulation_domain("Domain_device_concat")
[Schroedinger("d1:drain_Self_energy_schroed0")] initializing...
[Schroedinger("d1:drain_Self_energy_schroed0")] creating k-space object
[Schroedinger("d1:drain_Self_energy_schroed0")] parallelization is done outside.
[Schroedinger("d1:drain_Self_energy_schroed1")] initializing...
[Schroedinger("d1:drain_Self_energy_schroed1")] creating k-space object
[Schroedinger("d1:drain_Self_energy_schroed1")] parallelization is done outside.
[Schroedinger("d1:drain_Self_energy_schroed2")] initializing...
[Schroedinger("d1:drain_Self_energy_schroed2")] creating k-space object
[Schroedinger("d1:drain_Self_energy_schroed2")] parallelization is done outside.
[Schroedinger("d1:drain_Self_energy_schroed3")] initializing...
[Schroedinger("d1:drain_Self_energy_schroed3")] creating k-space object
[Schroedinger("d1:drain_Self_energy_schroed3")] parallelization is done outside.
[Schroedinger("d1:drain_Self_energy_schroed4")] initializing...
[Schroedinger("d1:drain_Self_energy_schroed4")] creating k-space object
[Schroedinger("d1:drain_Self_energy_schroed4")] parallelization is done outside.
[Schroedinger("d1:drain_Self_energy_schroed_global")] initializing...
[Schroedinger("d1:drain_Self_energy_schroed_global")] creating k-space object
[Schroedinger("d1:drain_Self_energy_schroed_global")] parallelization is done outside.
no options!
[Nemo] Simulation "d1:drain_Self_energy_result_propagation" of type "Self_Propagation" has been created.

    [Simulation] initializing boundary conditions...  boundary conditions are initialized.
[Schroedinger("d1:source_Self_energy_schroed0")] initializing...
[Schroedinger("d1:source_Self_energy_schroed0")] creating k-space object
[Schroedinger("d1:source_Self_energy_schroed0")] parallelization is done outside.
[Schroedinger("d1:source_Self_energy_schroed1")] initializing...
[Schroedinger("d1:source_Self_energy_schroed1")] creating k-space object
[Schroedinger("d1:source_Self_energy_schroed1")] parallelization is done outside.
[Schroedinger("d1:source_Self_energy_schroed2")] initializing...
[Schroedinger("d1:source_Self_energy_schroed2")] creating k-space object
[Schroedinger("d1:source_Self_energy_schroed2")] parallelization is done outside.
[Schroedinger("d1:source_Self_energy_schroed3")] initializing...
[Schroedinger("d1:source_Self_energy_schroed3")] creating k-space object
[Schroedinger("d1:source_Self_energy_schroed3")] parallelization is done outside.
[Schroedinger("d1:source_Self_energy_schroed4")] initializing...
[Schroedinger("d1:source_Self_energy_schroed4")] creating k-space object
[Schroedinger("d1:source_Self_energy_schroed4")] parallelization is done outside.
[Schroedinger("d1:source_Self_energy_schroed_global")] initializing...
[Schroedinger("d1:source_Self_energy_schroed_global")] creating k-space object
[Schroedinger("d1:source_Self_energy_schroed_global")] parallelization is done outside.
no options!
[Nemo] Simulation "d1:source_Self_energy_result_propagation" of type "Self_Propagation" has been created.

    [Simulation] initializing boundary conditions...  boundary conditions are initialized.
Schroedinger("d1:drain_Self_energy_schroed0"): destroying...
Schroedinger("d1:drain_Self_energy_schroed1"): destroying...
Schroedinger("d1:drain_Self_energy_schroed2"): destroying...
Schroedinger("d1:drain_Self_energy_schroed3"): destroying...
Schroedinger("d1:drain_Self_energy_schroed4"): destroying...
Schroedinger("d1:drain_Self_energy_schroed_global"): destroying...
Schroedinger("d1:source_Self_energy_schroed0"): destroying...
Schroedinger("d1:source_Self_energy_schroed1"): destroying...
Schroedinger("d1:source_Self_energy_schroed2"): destroying...
Schroedinger("d1:source_Self_energy_schroed3"): destroying...
Schroedinger("d1:source_Self_energy_schroed4"): destroying...
Schroedinger("d1:source_Self_energy_schroed_global"): destroying...
Schroedinger("d1:schroedss"): destroying...
Schroedinger("d1:schroeddd"): destroying...
Schroedinger("d1:schroedd"): destroying...
Schroedinger("d1:schroeds"): destroying...
Schroedinger("d1:schroed1"): destroying...
[Nemo] The entire simulation took 13.4928 seconds.
Have a good day!

```
