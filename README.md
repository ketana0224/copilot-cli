# copilot-cli
参考 skill集
https://github.com/github/awesome-copilot/tree/main


# 実行例
copilot -p daily-briefing.agent.md -s --allow-all-tools


# スケジュール実行（Windows タスクスケジューラ）
以下は、毎日 07:00 に `C:\GitHub\copilot-cli` へ移動してから 2 コマンドを順番に実行し、
あわせて「スケジュール時刻を過ぎたら、できるだけ早く実行する（StartWhenAvailable）」を有効化する設定です。

```powershell
schtasks /Create /TN 'Copilot Daily Briefing' /SC DAILY /ST 07:00 /TR 'cmd.exe /c "cd /d C:\GitHub\copilot-cli && copilot -p daily-briefing.agent.md -s --allow-all-tools && copilot -p daily-briefing-detail.agent.md -s --allow-all-tools"' /F
$taskName = 'Copilot Daily Briefing'; $task = Get-ScheduledTask -TaskName $taskName; $settings = $task.Settings; $settings.StartWhenAvailable = $true; Set-ScheduledTask -TaskName $taskName -Settings $settings
```

確認:

```powershell
schtasks /Query /TN "Copilot Daily Briefing" /V /FO LIST
```

削除:

```powershell
schtasks /Delete /TN "Copilot Daily Briefing" /F
```
