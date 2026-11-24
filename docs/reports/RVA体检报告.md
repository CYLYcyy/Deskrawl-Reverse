# RVA 体检报告（由 `tools/scripts/rva_audit.py` 自动生成，勿手改）

- 命令：`python rva_audit.py --check --falsify`
- 当期 GameAssembly.dll SHA-256：`de0896d9f6a20ed7b4137198fef86ba6a029ce001e01617c9aae78c1682d4113`
- 旧构建 dump.cs 来源：`git show 3c42617:data/schema/dump.cs`
- 扫描：41 个文件 / 175 条地址字面量

## 0. 结论摘要

| 判定 | 条数 |
|---|---|
| 非地址（白名单/自动规则） | 52 |
| 仍有效（方法） | 54 |
| 仍有效（注释里的方法名已过期） | 17 |
| 仍有效（数据地址） | 1 |
| 已失效（已给出重算值） | 0 |
| 已失效（内联数据，只能改成方法级引用） | 0 |
| 已失效（重算候选不唯一） | 0 |
| 已失效（无法重算） | 0 |
| 已失效（数据地址已迁移） | 0 |
| 无法判定（人工确认） | 0 |
| 历史对照（有意保留的旧地址） | 14 |
| 弃用探针（理由已写入文档） | 37 |
| **合计** | **175** |

## 1. 已失效与重算值（写回源码前需人工复核）

| 文件:行 | 注释 | 旧址 | 判定 | 重算值 | 依据 |
|---|---|---|---|---|---|

## 2. 仍有效但注释需更新（地址对、名字过期）

| 文件:行 | 注释名 | 当期名 |
|---|---|---|
| `tools/deskrawl_calc/effects.py:272` | EquipmentEffect_AbilityChannelModifier.bzw | 注释名 EquipmentEffect_AbilityChannelModifier.bzw → 当期名 cdz；EquipmentEffect_AbilityChannelModifier::cdz(Player a) { }) Slot=4 |
| `tools/deskrawl_calc/engine.py:277` | Player.PrimaryStatValue | 注释名 Player.PrimaryStatValue → 当期名 ezd；SettingsManager::ezd() { }) Slot=None |
| `tools/deskrawl_gui/core/calc_service.py:575` | Player.BaseFieldToStat | 注释名 Player.BaseFieldToStat → 当期名 faj；SettingsManager::faj() { }) Slot=None |
| `tools/deskrawl_gui/core/memory_conversions.py:8` | Player.ffq | 注释名 Player.ffq → 当期名 fvx；Player::fvx(StatType a, List<ValueTuple<StatType, StatType, double, StatusEffectData>> conversions) { }) Slot=None |
| `tools/deskrawl_gui/core/profile.py:416` | Player.PrimaryStatValue | 注释名 Player.PrimaryStatValue → 当期名 ezd；SettingsManager::ezd() { }) Slot=None |
| `tools/deskrawl_gui/core/profile.py:449` | PanelStat | 注释名 PanelStat → 当期名 boc；Player::boc(StatType a) { }) Slot=10 |
| `tools/deskrawl_gui/core/profile.py:449` | ffq | 注释名 ffq → 当期名 fvx；Player::fvx(StatType a, List<ValueTuple<StatType, StatType, double, StatusEffectData>> conversions) { }) Slot=None |
| `tools/deskrawl_gui/selftest_fixture.py:144` | cjb | 注释名 cjb → 当期名 cot；RuneData::cot(int a, List<AbilityLevelGrant> b) { }) Slot=None |
| `tools/deskrawl_gui/widgets/target_editor.py:17` | TrainingDummy.bkk | 注释名 TrainingDummy.bkk → 当期名 bod；TrainingDummy::bod(StatType a) { }) Slot=11 |
| `tools/scripts/make_doc09.py:55` | UnityEngine.JsonUtility.ToJson | 注释名 UnityEngine.JsonUtility.ToJson → 当期名 Reset；WaitForSecondsRealtime::Reset() { }) Slot=8 |
| `tools/scripts/make_doc09.py:58` | jg.je.ewr | 注释名 jg.je.ewr → 当期名 fmc；ko::fmc(string a) { }) Slot=None |
| `tools/scripts/mem_probe.py:15` | SaveSystem.ehq | 注释名 SaveSystem.ehq → 当期名 eti；SaveSystem::eti(SaveContainer a) { }) Slot=None |
| `tools/scripts/mem_probe.py:16` | SaveSystem.ehn | 注释名 SaveSystem.ehn → 当期名 etf；SaveSystem::etf(string a) { }) Slot=None |
| `tools/scripts/mem_probe.py:17` | SaveSystem.ehl | 注释名 SaveSystem.ehl → 当期名 etd；SaveSystem::etd(CharacterMode a) { }) Slot=None |
| `tools/scripts/mem_probe.py:18` | SaveSystem.eih | 注释名 SaveSystem.eih → 当期名 etz；SaveSystem::etz() { }) Slot=None |
| `tools/scripts/probe_player_statistics.py:7` | fpb | 注释名 fpb → 当期名 ftk；Inventory::ftk() { }) Slot=None |
| `tools/scripts/probe_runes.py:4` | ebx | 注释名 ebx → 当期名 emo；RuneManager::emo() { }) Slot=None |

## 3. 白名单：判为非地址（每条必须写明理由）

| 文件:行 | 字面量 | 理由 |
|---|---|---|
| `tools/deskrawl_calc/stattype.py:126` | `0x402010` | 封顶属性的**位掩码**（注释原文「掩码 0x402010 + 特判 37」），是 4 项封顶属性的位集，不是地址；与之配对的 0x4A9C30 才是代码地址 |
| `tools/deskrawl_gui/app.py:804` | `0xC0000409` | 值 0xC0000409 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/deskrawl_gui/core/glossary.py:51` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/deskrawl_gui/core/memory_reader.py:5` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/deskrawl_gui/core/memory_reader.py:22` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/deskrawl_gui/core/memory_reader.py:48` | `0x10000` | 用户态指针下限，出现在 `0x10000 <= p < 0x7FFFFFFEFFFF` 的范围比较里，是阈值不是地址 |
| `tools/deskrawl_gui/core/memory_reader.py:163` | `0x1000` | PROCESS_QUERY_LIMITED_INFORMATION 权限常量（OpenProcess 的 dwDesiredAccess 参数），是访问掩码不是地址 |
| `tools/deskrawl_gui/core/memory_reader.py:298` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/deskrawl_gui/core/memory_reader.py:299` | `0x100000000` | 值 0x100000000 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/deskrawl_gui/core/memory_reader.py:299` | `0x80000000` | 值 0x80000000 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/deskrawl_gui/core/memory_reader.py:322` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/deskrawl_gui/core/memory_reader.py:337` | `0xFF0000FF` | 值 0xFF0000FF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/deskrawl_gui/selftest_effects.py:29` | `0x1234` | 同上：面板复算自检里「需带状态才生效的换算」用非空状态指针占位，验证跳过 + 告警，不指向任何目标 |
| `tools/deskrawl_gui/selftest_robustness.py:279` | `0x7FF00000` | 值 0x7FF00000 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/deskrawl_gui/selftest_robustness.py:288` | `0x7FF00000` | 值 0x7FF00000 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/deskrawl_gui/selftest_skillmods.py:22` | `0x100000` | 自检用的**合成指针**：0x100000 只验证「第 i 个技能指针 ↔ 第 i 个名字」的展开位置，0x1234 是非空状态指针的占位（验证「带 RequiredStatus 的换算条目要丢弃」），都不指向游戏里的任何目标 |
| `tools/deskrawl_gui/selftest_skillmods.py:30` | `0x100000` | 自检用的**合成指针**：0x100000 只验证「第 i 个技能指针 ↔ 第 i 个名字」的展开位置，0x1234 是非空状态指针的占位（验证「带 RequiredStatus 的换算条目要丢弃」），都不指向游戏里的任何目标 |
| `tools/deskrawl_gui/selftest_skillmods.py:111` | `0x1234` | 自检用的**合成指针**：0x100000 只验证「第 i 个技能指针 ↔ 第 i 个名字」的展开位置，0x1234 是非空状态指针的占位（验证「带 RequiredStatus 的换算条目要丢弃」），都不指向游戏里的任何目标 |
| `tools/scripts/decode.py:96` | `0xFF0000FF` | 值 0xFF0000FF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/decode.py:100` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/decode.py:125` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/decode.py:125` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/decode.py:128` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/disasm.py:11` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |
| `tools/scripts/disasm2.py:9` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |
| `tools/scripts/disasm2.py:95` | `0x8000000` | 值 0x8000000 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/dump_index.py:91` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/dump_index.py:147` | `0x4000` | `containing()` 判定「内联数据是否属于该方法的跨距阈值」，是搜索窗口宽度不是地址 |
| `tools/scripts/extract_rolltable.py:11` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |
| `tools/scripts/mem_probe.py:37` | `0x0400` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/mem_probe.py:38` | `0x0010` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/mem_probe.py:65` | `0x10000` | 同上（内存链刻意自包含，与 memory_reader.py 是两份独立实现） |
| `tools/scripts/mem_probe.py:222` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/mem_probe.py:223` | `0x100000000` | 值 0x100000000 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/mem_probe.py:223` | `0x80000000` | 值 0x80000000 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/mem_probe.py:235` | `0xFFFFFFFF` | 值 0xFFFFFFFF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/mem_probe.py:261` | `0xFF0000FF` | 值 0xFF0000FF 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/mem_probe.py:559` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/obs_solve3.py:42` | `0xffffffff` | 值 0xffffffff 超出映像范围（max_rva=0x42a2e00），是掩码/哨兵而非地址 |
| `tools/scripts/pe_file.py:8` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |
| `tools/scripts/probe_dps_meter.py:34` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/probe_paragon.py:41` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/probe_paragon.py:45` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |
| `tools/scripts/probe_player_statistics.py:28` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/probe_runes.py:37` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/probe_skill_levels.py:9` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/probe_stat_labels.py:47` | `0x0410` | 四位以内的微常量（位掩码/计数/标志），不可能是地址 |
| `tools/scripts/probe_stat_labels.py:51` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |
| `tools/scripts/rea_call.py:60` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |
| `tools/scripts/read_const.py:6` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |
| `tools/scripts/rva_audit.py:518` | `0x1000` | 本脚本的「微常量上限」判定阈值（低于它的字面量直接归入非地址），是规则参数不是地址 |
| `tools/scripts/xref.py:7` | `0x180000000` | PE ImageBase 本身（节表换算基准），不是可寻址目标 |

## 4a. 仍有效（数据地址：常量新址 / 当期 script.json 槽 / 登记的数据指针）

| 文件:行 | 字面量 | 依据 |
|---|---|---|
| `tools/deskrawl_calc/engine.py:178` | `0x1837353C0` | 常量「护甲分母」= 50.0（double） |

## 4b. 历史对照（紧邻「旧/补丁前」标注，刻意保留的旧地址）

| 文件:行 | 字面量 | 原判定 | 重算值 | 上下文 |
|---|---|---|---|---|
| `tools/deskrawl_calc/cli.py:65` | `0x509D80` | 无法判定（人工确认） | — | `CalcDamage@0x5670C0，补丁前 bjr@` |
| `tools/deskrawl_calc/engine.py:178` | `0x18363F120` | 无法判定（人工确认） | — | `el))。常量 50 @ 0x1837353C0（补丁前` |
| `tools/deskrawl_calc/stattype.py:107` | `0x6F6360` | 无法判定（人工确认） | — | `nit @ 0x79AFF0，补丁前 ..cctor @` |
| `tools/scripts/mem_probe.py:15` | `0x7BA6A0` | 无法判定（人工确认） | — | `       RVA 0x84BD50   （旧 egi` |
| `tools/scripts/mem_probe.py:16` | `0x7BA220` | 无法判定（人工确认） | — | `       RVA 0x84B8D0   （旧 egf` |
| `tools/scripts/mem_probe.py:17` | `0x7B9E00` | 无法判定（人工确认） | — | `       RVA 0x84B4B0   （旧 egd` |
| `tools/scripts/mem_probe.py:18` | `0x7BBFD0` | 无法判定（人工确认） | — | `       RVA 0x84D680   （旧 egz` |
| `tools/scripts/mem_probe.py:170` | `0x7C7350` | 无法判定（人工确认） | — | `ehq(SaveContainer)   旧 egi',` |
| `tools/scripts/mem_probe.py:171` | `0x7C6ED0` | 无法判定（人工确认） | — | `ehn(string)          旧 egf',` |
| `tools/scripts/mem_probe.py:172` | `0x7C6AB0` | 无法判定（人工确认） | — | `ehl(CharacterMode)   旧 egd',` |
| `tools/scripts/mem_probe.py:173` | `0x7C8C80` | 无法判定（人工确认） | — | `eih()                旧 egz',` |
| `tools/scripts/mem_probe.py:179` | `0x77D960` | 无法判定（人工确认） | — | `'GameManager.dlo()   旧 dkg',` |
| `tools/scripts/mem_probe.py:180` | `0x4FD1D0` | 无法判定（人工确认） | — | `'Inventory.fdi()     旧 fbq',` |
| `tools/scripts/mem_probe.py:181` | `0x52B390` | 无法判定（人工确认） | — | `'Storage.frm()       旧 fpi',` |

## 4c. 弃用探针（不参与生产路径，理由与出处见文档；原判定与重算值仍保留）

| 文件:行 | 字面量 | 原判定 | 重算值 | 文档 |
|---|---|---|---|---|
| `tools/scripts/chk.py:26` | `0x39E4408` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/chk.py:26` | `0x39E4410` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/chk.py:26` | `0x39E4470` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/chk.py:26` | `0x39E4478` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/chk.py:26` | `0x39E44B0` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/chk.py:26` | `0x39E44C8` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/meta_range.py:6` | `0x39E43C0` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/meta_range.py:6` | `0x39E44E0` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/probe_paragon.py:17` | `0x183A62170` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/probe_stat_labels.py:13` | `0x183A64B90` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/probe_stat_labels.py:13` | `0x183A66578` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/probe_stat_labels.py:13` | `0x183A66570` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/probe_stat_labels.py:14` | `0x183A6E7C8` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/probe_stat_labels.py:14` | `0x183A58008` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/probe_stat_labels.py:14` | `0x183A5D560` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/probe_stat_labels.py:15` | `0x183A64BE8` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:29` | `0x18362a1a0` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:30` | `0x18362a0e0` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:31` | `0x183629f64` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:32` | `0x183629ff8` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:33` | `0x18362a028` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:34` | `0x18362a050` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:35` | `0x18362a160` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:36` | `0x18362a658` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:37` | `0x183629e40` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/read_const.py:38` | `0x18362a3c0` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/strings_ctx.py:14` | `0x36f10` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/strings_ctx.py:14` | `0xbfe9b` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/strings_ctx.py:14` | `0xc0b56` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/strings_ctx.py:14` | `0x90167` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/strings_ctx.py:14` | `0x61685b` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/xref.py:45` | `0x1839e44c8` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/xref.py:46` | `0x1839e44b0` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/xref.py:47` | `0x1839e4470` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/xref.py:48` | `0x1839e4478` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/xref.py:49` | `0x1839e4408` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |
| `tools/scripts/xref.py:50` | `0x1839e4410` | 无法判定（人工确认） | — | docs/plan/补丁回归清单.md |

弃用理由（配置里声明，脚本已校验文档确实写了）：

- `tools/scripts/chk.py`：一次性 PE 查看器：RVA 列表是取样（.data 里 SaveFileWriter/DDS1/DDS2 那批），不是锚点；且其功能已被 pe_file.py（节表/换算/读字节）覆盖。补丁后取样地址语义已变，重锚定无价值。
- `tools/scripts/meta_range.py`：一次性范围取样（[0x39E43C0,0x39E44E0] 打印 ScriptString），功能已被 script_index.py 完整覆盖；范围边界是取样窗口而非锚点。
- `tools/scripts/probe_paragon.py`：1.0.3 巅峰点数状态槽的实机探针：STATE_SLOT_VA 是当次 PE 取样得到的 .data 元数据槽地址，原始输入（补丁前 DLL）已被 1.0.4 覆盖且无当期 dump 可唯一定位。其职能已由 dump_index/script_index 承接，待需要时按当期构建重新实机取样。
- `tools/scripts/probe_stat_labels.py`：1.0.3 属性标签字面量的实机取样探针：hnk/hnm 那批 .data 槽地址是当次 PE 字节取样结果，原始输入（补丁前 DLL）已覆盖，静态无法唯一定位。标签表职能已由 script_index.py + 当期 script.json 承接。
- `tools/scripts/read_const.py`：一次性常量探针：目标常量在旧常量簇 0x18362A***，标签本身带问号（'roll_high / default(1.0?)'），且原始输入（补丁前 GameAssembly.dll）已被游戏更新覆盖，不可复原。其任务已由 extract_rolltable.py + docs/08 §11.3 的 55 项系数表 + §12.2 新址表承接。
- `tools/scripts/strings_ctx.py`：探针输入是 global-metadata.dat 的文件偏移，补丁后该文件被覆盖（同版本 v39、内容不同），旧偏移不可复原；当时的结论（SerializeReference 托管段布局）已固化进 decode.py 与 docs/08 §11.1。
- `tools/scripts/xref.py`：一次性 xref 探针：6 个目标地址是手搓的，与补丁前 script.json 的字面量表并不一致（'password' 项 0x39E44C8 vs 表内 0x39F1AD0），本身就不可信；字符串地址的权威来源已改为 script_index.py + script.json。

## 5. 文档表格复核

### 5.1 docs/08 §12.1 PE 节表

| 节 | 文档 VA | 实测 VA | 文档 raw | 实测 raw | 结论 |
|---|---|---|---|---|---|
| `.text` | `0x180001000` | `0x180001000` | `0x400` | `0x400` | ✅ |
| `il2cpp` | `0x18042d000` | `0x18042d000` | `0x42be00` | `0x42be00` | ✅ |
| `.rdata` | `0x182f23000` | `0x182f23000` | `0x2f21c00` | `0x2f21c00` | ✅ |
| `.data` | `0x183a3d000` | `0x183a3d000` | `0x3a3b800` | `0x3a3b800` | ✅ |

### 5.2 docs/08 §9.1+§12.2 常量新旧址（新址必须逐字节读回该值）

| 常量 | 值 | 旧址读取 | 新址 | 新址读取 | 结论 |
|---|---|---|---|---|---|
| 命中浮动上界 | `1.1` | `double=2.65058494311186e-310 float32=1.750361911788129e-41` | `0x1837351fc` | `double=0.015234442414657679 float32=1.100000023841858` | ✅ |
| 受伤阈值 | `0.3` | `double=1.3930902375612e-310 float32=2.2476827367770066e-41` | `0x183735260` | `double=0.3 float32=4.17232506322307e-08` | ✅ |
| 健康阈值 | `0.8` | `double=3.34957035683116e-310 float32=2.2476827367770066e-41` | `0x1837352b8` | `double=0.8 float32=-1.5881868392106856e-23` | ✅ |
| 属性数值封顶 | `0.85` | `double=3.4036812495008e-310 float32=2.2476827367770066e-41` | `0x1837352c0` | `double=0.85 float32=4.17232506322307e-08` | ✅ |
| 命中浮动下界 | `0.9` | `double=3.4036812495008e-310 float32=2.2476827367770066e-41` | `0x1837352c8` | `double=0.9 float32=-107374184.0` | ✅ |
| 易伤乘区 | `1.3` | `double=1.05357091045956e-310 float32=6.957446875372717e-42` | `0x1837352f8` | `double=1.3 float32=-107374184.0` | ✅ |
| 护甲分母 | `50.0` | `double=2.63679197015087e-310 float32=8.435816755235399e-42` | `0x1837353c0` | `double=50.0 float32=0.0` | ✅ |
| 主属性分母 | `100.0` | `double=2.6367919701481e-310 float32=8.357344041233209e-42` | `0x1837353d8` | `double=100.0 float32=0.0` | ✅ |

## 6. memory_offsets.json 复核（结构偏移与方法锚点）

| 配置路径 | 模式 | 命中 | 说明 |
|---|---|---|---|
| `player` | field | ✅ | 全部命中 |
| `player` | field | ✅ | 全部命中 |
| `player.stat_dicts` | field | ✅ | 全部命中 |
| `player.conditional_mods` | field | ✅ | 全部命中 |
| `player.status_controller` | field | ✅ | 全部命中 |
| `player.status_controller` | field | ✅ | 全部命中 |
| `hero_data` | field | ✅ | 全部命中 |
| `inventory_slot` | field | ✅ | 全部命中 |
| `item_data` | field | ✅ | 全部命中 |
| `generated_item` | field | ✅ | 全部命中 |
| `talent_effect_ability_modifier` | field | ✅ | 全部命中 |
| `player.conditional_mods` | const | ✅ | 结构尺寸与声明一致 |
| `talent_effect_conditional_stat` | const | ✅ | 结构尺寸与声明一致 |
| `talent_effect_stat_conversion` | field | ✅ | 全部命中 |
| `player_conversions` | field | ✅ | 全部命中 |
| `player_conversions` | const | ✅ | 结构尺寸与声明一致 |
| `talent_effect_ability_modifier` | const | ✅ | 结构尺寸与声明一致 |
| `singleton_getters` | rva | ✅ | 全部命中 |
| `save_system.anchor_rvas` | rva | ✅ | 全部命中 |
| `generated_items.klass` | klass | ✅ | 类 GameConfig 仍存在 |
| `hero_data.klass` | klass | ✅ | 类 HeroData 仍存在 |
| `item_data.klass` | klass | ✅ | 类 ItemData 仍存在 |
| `generated_item_klass` | klass | ✅ | 类 GeneratedItemData 仍存在 |

### 6.1 版本指纹门禁

| 键 | 声明值 | 实测值 | 结论 |
|---|---|---|---|
| `game_assembly_sha256` | `de0896d9f6a20ed7…` | `de0896d9f6a20ed7…` | ✅ |
| `global_metadata_sha256` | `6637c2fcf57dc7d8…` | `6637c2fcf57dc7d8…` | ✅ |

## 7. 可证伪演示（`--falsify`）

| 用例 | 期望 | 实测 | 结论 | 说明 |
|---|---|---|---|---|
| `0x180567341` | stale | unknown | ✅ | Character.CalcDamage 当期 0x1805670C0 末位+1，必须判失效 |
| `0x1805670C1` | stale | unknown | ✅ | Player.CalcDamage 当期 0x1805670C0 末位+1 |
| `0x84BD51` | stale | unknown | ✅ | SaveSystem.SerializeContainer 当期 0x84BD50 末位+1（RVA） |
| `0x1837352C1` | stale | unknown | ✅ | 常量 0.85 新址 0x1837352C0 末位+1（数据地址） |
| `0x183A62171` | stale | unknown | ✅ | 当期元数据槽末位+1：当期表查不到，必须落回人工确认 |
| `0x1805670C0` | valid | valid | ✅ | 真值对照：当期 Player.CalcDamage 必须判有效 |

## 8. 配置与文档锚点自校验

### 8.1 `data_refs` 逐条锚点（没有可核对锚点的必须显式声明 `anchor: none`）

| 文件 | 字面量 | 锚点 | 结论 | 说明 |
|---|---|---|---|---|
| `tools/scripts/probe_paragon.py` | `0x183A62170` | 名字核对 | ✅ | expect=hk_TypeInfo |
| `tools/scripts/probe_stat_labels.py` | `0x183A64B90` | 名字核对 | ✅ | expect=ItemRarity_var |
| `tools/scripts/probe_stat_labels.py` | `0x183A66578` | 名字核对 | ✅ | expect=Method$UnityEngine.Object.Instantiate<StatRowUI>() |
| `tools/scripts/probe_stat_labels.py` | `0x183A66570` | 名字核对 | ✅ | expect=StatRowUI[]_TypeInfo |
| `tools/scripts/probe_stat_labels.py` | `0x183A6E7C8` | 名字核对 | ✅ | expect=ItemRarity[]_TypeInfo |
| `tools/scripts/probe_stat_labels.py` | `0x183A58008` | 名字核对 | ✅ | expect=UnityEngine.Object_TypeInfo |
| `tools/scripts/probe_stat_labels.py` | `0x183A5D560` | 名字核对 | ✅ | expect=GameManager_TypeInfo |
| `tools/scripts/probe_stat_labels.py` | `0x183A64BE8` | 名字核对 | ✅ | expect=PlayerStatistics_TypeInfo |
| `docs/08-常量设计要点与待办.md` | `0x182F19730` `0x1834DE720` | 显式无锚点 | ✅ | 已声明当期无锚点可查（原因写在 reason 里） |
| `docs/08-常量设计要点与待办.md` | `0x183681510` `0x183681508` `0x183681518` `0x183681978` | 显式无锚点 | ✅ | 已声明当期无锚点可查（原因写在 reason 里） |

### 8.2 文档记录的构建指纹（文档 ↔ 磁盘 双向核对）

| 键 | 文档 | 文档记录值 | 磁盘实测 | 结论 |
|---|---|---|---|---|
| `game_assembly_sha256` | `docs/08-常量设计要点与待办.md` | `de0896d9f6a20ed7…` | `de0896d9f6a20ed7…` | ✅ 与磁盘一致；文档已记录 |

