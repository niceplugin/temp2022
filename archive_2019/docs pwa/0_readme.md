# 기본구조

1. `serviceWorkerContainer.register()`을 통해서 서비스 워커 URL을 가져오고, 등록합니다.

1. 등록에 성공하면, `ServiceWorkerGlobalScope` 범위에서 서비스 워커가 실행됩니다. 이는 (메인 스크립트 실행 쓰레드를 running off하면서) 기본적으로 DOM 접근이 없는 작업 문맥을 갖습니다.

1. 이제 서비스 워커는 이벤트를 처리할 준비가 되었습니다.

1. 서비스 워커가 제어하는 페이지들에 연속적으로 접근하게 될 때 서비스 워커 설치를 시도하게 됩니다. 서비스 워커는 항상 처음으로 설치 이벤트를 받습니다.(설치 이벤트는 IndexedDB를 생성하고, 사이트 assets을 캐싱하는 처리를 시작할 때 사용될 수 있습니다.) 설치 이벤트는 모든 것을 오프라인에서 사용할 수 있게 하는, 네이티브 또는 파이어폭스 OS 앱을 설치하는 프로시저와 같은 종류입니다.

1. `oninstall` 핸들러가 완료되면, 서비스 워커가 설치되었다고 할 수 있습니다.

1. 다음은 활성(activation) 이벤트입니다. 서비스 워커가 설치되면, 활성 이벤트를 받게 됩니다. `onactivate`는 이전 버전의 서비스 워커 스크립트에서 사용된 리소스들을 삭제하는 용도로서 주로 사용됩니다.

1. 이제 서비스 워커가 페이지들을 제어하게 될 것이지만, 오직 `register()` 가 성공적으로 수행된 후에 페이지들이 열리게 될 것입니다. 즉, 문서는 서비스 워커와 함께, 또는 없이도 라이프를 시작하고 유지합니다. 따라서 문서는 실제로 서비스 워커에 제어되기 위해서 재시작 되어야 할 것입니다.