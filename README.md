# JDA-Luffia
해당 봇을 사용하여 디스코드 봇으로 여러 음성채팅방에서 노래 재생, 이메일 본인인증, 게임 전적 검색 기능을 서비스 할 수 있습니다

## Information
이 봇은 Discord bagkaseu(박카스#9970) 에 의해 제작되었습니다.

* 해당 봇의 오류나 건의, 문의사항이 있을시 제작자에게 문의 또는 [Issue](https://github.com/Backas03/JDA-Luffia/issues) 바랍니다.

* 모든 Pull Request 코드에는 시작과 끝 부분에 아래 형식과 같이 표기하여야 합니다. 아래는 예시입니다. </br>
  [[../kr/kro/backas/Luffia.java]](https://github.com/Backas03/JLuffia/blob/master/src/main/java/kr/kro/backas/Luffia.java)
  ```java
  public Luffia(JDA discordAPI) throws IOException {
    this.discordAPI = discordAPI;
  
    this.commandManager = new CommandManager("!", discordAPI);
    this.commandManager.registerCommand("인증", new CertificationCommand());
    this.commandManager.registerCommand("정보", new CertificationInfoCommand());
    this.commandManager.registerCommand("인증해제", new CertificationRemoveCommand());
    this.commandManager.registerCommand("도움말", new HelpCommand());

    this.certificationManager = new CertificationManager(discordAPI);
  
    아래 4줄이 PR에서 추가된 부분 입니다
    /* [backas03] add command start */
    this.commandManager.registerCommand("테스트1", null);
    this.commandManager.registerCommand("테스트2", null);   
    /* [backas03] add command end */      

    this.discordAPI.getPresence().setActivity(Activity.playing("!도움말 명령어로 기능 확인"));
  }
  ```
## 봇 사용방법
1. src/main/java/kr/kro/backas/secret/ 폴더에 BotSecret.java 파일을 추가합니다
2. 아래를 완성합니다
- src/main/java/kr/kro/backas/secret/BotSecret.java
```java
package kr.kro.backas.secret;

import java.util.List;

public final class BotSecret {
    // 대학교 인증 메일을 보내기 위한 구글 이메일 ID
    public static final String EMAIL = "emailcert@gmail.com";

    // 대학교 인증 메일을 보내기 위한구글 이메일 앱 비밀번호
    public static final String APP_PASSWORD = "asdqgdavxqwekwa";

    // 봇 토큰
    public static final String TOKEN = "AAA5NfMasdzwqeqw4MTM2NzExMg.GasdfgO.XijzuasdJDoasdfgOZzeeKNQ6tRz_I";

    // SharedConstant.ON_DEV == true 일때 사용할 봇 토큰 (입력하지 않아도 됩니다)
    public static final String DEV_TOKEN = "";

    // 롤 전적 검색 기능을 위한 라이엇 API key
    public static final String RIOT_API_KEY = "RGAPI-6asdhgas79-0qw1-4aa1-98dd-ede3asda137d76";

    // 하나의 서버에 여러 음성채팅방에서 음악을 재생시키기 위한 봇 토큰
    public static final List<String> MUSIC_BOT_TOKENS = List.of(
            "ggg1MzI1MzkasdExODMwNA.Gm3wvS.sfasfas4pPi9d_a4zrqHClEp3IxPpqkGWrYQ3h1t-Tk", // bot 1 (해당 토큰은 실제 존재하지 않는 토큰입니다)
            "eeeasdNzQ2NTEyNzAzNDg4MA.G6etwH.CSwxF9TkKeosfasfasfasasrqwrw" // bot 2 (해당 토큰은 실제 존재하지 않는 토큰입니다)
    );
}
```
3. SharedConstant.java 에서 MAIN_GUILD_ID 를 서비스 할 서버 guild id로 수정합니다 </br>
해당 서버에서만 명령어를 작동하도록 설정하는 부분으로, 수정하지 않으면 명령어가 작동하지 않습니다.
- kr/kro/backas/SharedConstant.java
```java
package kr.kro.backas;

public final class SharedConstant {
    public static final long MAIN_GUILD_ID = 791974345965961237L; // 봇을 초대할 서버 id 로 변경

    public static final long DEV_GUILD_ID = 1121632283154202694L;
    public static final long PUBLISHED_GUILD_ID = MAIN_GUILD_ID;

    public static final boolean ON_DEV = false;

    public static final String RELEASE_VERSION = "Luffia/2.1.0-Stable-Release";

    public static final String LICENSE = "MIT license";

    public static final String GITHUB = "https://github.com/Backas03/JDA-Luffia";
}
```
4. 봇을 실행하려면 ```./gradlew run``` 을 입력합니다 </br>
![image](https://github.com/Backas03/JDA-Luffia/assets/71801733/b0b3160c-d048-433a-b56d-f2349edc7306)
## 기능 소개
1. 대학교 인증 기능
- 대학교 이메일로 인증 코드를 받아 학교 인증을 진행 할 수 있습니다
- 해당 기능을 사용하여 인증 역할을 부여할 수 있습니다
지원 명령어
```
/인증 :학교 이메일: - 해당 학교 이메일로 인증 코드를 전송받습니다

---- 관리자 명령어 ----
!인증해제 [userId] - 해당 유저의 인증 데이터를 해제합니다.
!인증정보 [userId] - 해당 유저의 인증 데이터를 확인합니다.
!강제인증 [userId] [학교 이메일] - 해당 유저를 관리자의 권한으로 강제 인증시킵니다.
```
![image](https://github.com/Backas03/JDA-Luffia/assets/71801733/3893ce5e-ec5d-41b6-b208-baae0970d518)
![image](https://github.com/Backas03/JDA-Luffia/assets/71801733/938c3751-957c-4a38-aaae-43f726eb01a6)
3. 뮤직 플레이어 기능
LavaPlayer 라이브러리를 사용하여 유튜브에서 노래를 검색 후 디스코드에서 음악을 재생할 수 있습니다 </br>
![image](https://github.com/Backas03/JDA-Luffia/assets/71801733/8850d664-b12c-4569-b403-59e358bb796c) </br>
추가적으로 봇을 추가하여 하나의 디코방에서 여려 음성채팅방에서 음악을 재생할 수 있습니다 (봇 상태메시지에 현재 재생중인 음성채팅방의 이름을 표기합니다) </br>
![image](https://github.com/Backas03/JDA-Luffia/assets/71801733/95db993f-c22c-4c16-86cd-f8f3a28da4b5) </br>
해당 기능을 사용하기 위해서는 secret/BotSecret.java 파일 생성 후 public static final List<String> MUSIC_BOT_TOKENS 항목에 값을 추가해주시면 됩니다 </br>
- secret/BotSecret.java
``` java
public static final List<String> MUSIC_BOT_TOKENS = List.of(
            "MTE1MzI1MzkasdExODMwNA.Gm3wvS.sfasfas4pPi9d_a4zrqHClEp3IxPpqkGWrYQ3h1t-Tk", // bot 1 (해당 토큰은 실제 존재하지 않는 토큰입니다)
            "MTEasdNzQ2NTEyNzAzNDg4MA.G6etwH.CSwxF9TkKeosfasfasfasasrqwrw" // bot 2 (해당 토큰은 실제 존재하지 않는 토큰입니다)
);
```


5. 게임 전적 검색 기능 </br>
- !롤정보 [닉네임] 으로 정보를 검색할 수 있습니다 </br>
![image](https://github.com/Backas03/JDA-Luffia/assets/71801733/6d5395d0-db25-4b94-bb34-c98561824c17) </br>
- !메이플정보 [닉네임] 으로 정보를 검색할 수 있습니다 (unstable) </br>
![image](https://github.com/Backas03/JDA-Luffia/assets/71801733/6c12ac59-bbda-4cab-a40c-f8dbcb10181c)

## 명령어 비활성화 방법
Luffia.java에서 this.commandManager.registerCommand를 주석처리하면 됩니다
- kr/kro/backas/Luffia.java
```java
public Luffia(JDA discordAPI) throws IOException, InterruptedException {
    this.discordAPI = discordAPI;

    this.commandManager = new CommandManager("!", this);

    this.commandManager.registerSlashCommand(new SlashCertificationCommand());

    this.commandManager.registerCommand("인증정보", new CertificationInfoCommand());
    this.commandManager.registerCommand("인증해제", new CertificationRemoveCommand());
    this.commandManager.registerCommand("도움말", new HelpCommand());
    this.commandManager.registerCommand("강제인증", new ForceCertificationCommand());

    this.commandManager.registerCommand("재생", new PlayCommand());
    this.commandManager.registerCommand("나가기", new QuitCommand());
    this.commandManager.registerCommand("스킵", new SkipCommand());
    this.commandManager.registerCommand("일시정지", new PauseCommand());
    this.commandManager.registerCommand("일시정지해제", new ResumeCommand());
    //this.commandManager.registerCommand("전체반복", new RepeatAllCommand()); // 비활성화
    //this.commandManager.registerCommand("반복", new RepeatCurrentCommand()); // 비활성화
    //this.commandManager.registerCommand("반복해제", new NoRepeatCommand()); // 비활성화
    this.commandManager.registerCommand("대기열", new QueueCommand());

    this.commandManager.registerCommand("롤정보", new LOLUserInfoCommand());

    this.commandManager.registerCommand("메이플정보", new MapleUserInfoCommand());

    this.certificationManager = new CertificationManager(discordAPI);

    this.musicPlayerController = new MusicPlayerController();
    discordAPI.addEventListener(this.musicPlayerController);
    for (String botToken : BotSecret.MUSIC_BOT_TOKENS) {
        this.musicPlayerController.register(botToken);
    }


    this.discordAPI.addEventListener(new MusicListener());
    this.discordAPI.addEventListener(new CertificationListener());
    this.discordAPI.getPresence().setActivity(Activity.playing("!도움말 명령어로 기능 확인"));
}
```
## 커멘드 prefix 변경방법
Luffia.java에서 this.commandManager = new CommandManager("!", this); 의 "!" 부분을 원하는 prefix로 변경하면 됩니다.
- kr/kro/backas/Luffia.java
```java
public Luffia(JDA discordAPI) throws IOException, InterruptedException {
    this.discordAPI = discordAPI;

    /*
     * 커멘드 prefix를 ! 에서 && 으로 변경.
     * ex) !인증정보 >> &&인증정보
     */ 
    this.commandManager = new CommandManager("&&", this);

    this.commandManager.registerSlashCommand(new SlashCertificationCommand());

    this.commandManager.registerCommand("인증정보", new CertificationInfoCommand());
    this.commandManager.registerCommand("인증해제", new CertificationRemoveCommand());
    this.commandManager.registerCommand("도움말", new HelpCommand());
    this.commandManager.registerCommand("강제인증", new ForceCertificationCommand());

    this.commandManager.registerCommand("재생", new PlayCommand());
    this.commandManager.registerCommand("나가기", new QuitCommand());
    this.commandManager.registerCommand("스킵", new SkipCommand());
    this.commandManager.registerCommand("일시정지", new PauseCommand());
    this.commandManager.registerCommand("일시정지해제", new ResumeCommand());
    //this.commandManager.registerCommand("전체반복", new RepeatAllCommand());
    //this.commandManager.registerCommand("반복", new RepeatCurrentCommand());
    //this.commandManager.registerCommand("반복해제", new NoRepeatCommand());
    this.commandManager.registerCommand("대기열", new QueueCommand());

    this.commandManager.registerCommand("롤정보", new LOLUserInfoCommand());

    this.commandManager.registerCommand("메이플정보", new MapleUserInfoCommand());

    this.certificationManager = new CertificationManager(discordAPI);

    this.musicPlayerController = new MusicPlayerController();
    discordAPI.addEventListener(this.musicPlayerController);
    for (String botToken : BotSecret.MUSIC_BOT_TOKENS) {
        this.musicPlayerController.register(botToken);
    }


    this.discordAPI.addEventListener(new MusicListener());
    this.discordAPI.addEventListener(new CertificationListener());
    this.discordAPI.getPresence().setActivity(Activity.playing("!도움말 명령어로 기능 확인"));
}
```
