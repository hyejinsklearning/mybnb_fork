# meetingroom




# 서비스 시나리오

회의실 예약/상태 관리

기능적 요구사항
1. 관리자가 회의실 목록을 조회한다.
1. 관리자가 회의실을 신규 등록한다.
1. 관리자가 회의실 정보를 변경한다.

1. 사용자가 회의실를 선택하여 회의실을 예약한다.
1. 사용자가 결제한다. (Sync, 결제서비스)
1. 결제가 완료되면, 예약 내용을 사용자에게 전달한다. (Async, 통지서비스)
1. 예약 내역이 관리자에게 전달된다.

1. 사용자는 본인의 예약/사용 등 상태를 조회한다.
1. 사용자가 예약을 취소할 수 있다.
1. 예약이 취소되면, 결제를 취소한다. (Sync, 결제서비스)

1. 사용자가 회의실 사용을 시작한다.
1. 사용자가 회의실 사용을 완료한다.
1. 회의실 사용 상태가 변경될 때마다 사용자에게 알림을 보낸다. (Async, 통지서비스)
1. 관리자는 전체 회의실의 예약/사용 등의 상태를 조회한다.

비기능적 요구사항
1. 트랜잭션
    1. 결제가 되지 않은 예약건은 아예 거래가 성립되지 않아야 한다  Sync 호출 
1. 장애격리
    1. 통지(알림) 기능이 수행되지 않더라도 예약은 365일 24시간 받을 수 있어야 한다  Async (event-driven), Eventual Consistency
    1. 결제시스템이 과중되면 사용자를 잠시동안 받지 않고 결제를 잠시후에 하도록 유도한다  Circuit breaker, fallback
1. 성능
    1. 고객이 자주 예약관리에서 확인할 수 있는 상태를 마이페이지(프론트엔드)에서 확인할 수 있어야 한다  CQRS
    1. 처리상태가 바뀔때마다 카톡 등으로 알림을 줄 수 있어야 한다  Event driven