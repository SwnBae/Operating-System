# Operating-System (리눅스)

# Report1 - Blocking, Non-Blocking방식을 활용한 Alarm clock의 개선
 기존 Pintos 커널에서 time_sleep()함수는 정상적으로 작동하지만, Busy waiting방식으로 구현되어 있습니
다. 이는 CPU를 낭비하므로 비효율을 초래합니다. 특히 타이머가 긴 시간 동안 대기해야 하는 경우에는 매
타이머 틱마다 체크하므로, CPU를 낭비하고 다른 프로세스나 스레드의 실행을 방해하며, 전력 소비도 증가
시킵니다.
 이러한 문제를 해결하기 위해 pintos 커널에 있는 timer.c의 timer_sleep()과 timer_interrupt()를 개선하는
방법을 사용합니다. alarm 구조체를 사용한 alarms를 더블 링크드 리스트 형태로 구현하고, 이를 활용하여
코드를 개선할 수 있습니다. 또한 alarm_compare함수를 추가로 구현하여 리스트의 순서를 항상 만료시간
기준 오름차순이 될 수 있도록 만들어줍니다. 이후 pintos에서 제공하는 test들을 통해 개선된 Alarm Clock
이 잘 작동되는지 확인합니다.
 이와 같은 과정을 통해, Alarm clock을 No Busy-wait형태로 구현할 수 있습니다.

# Report2 - Pintos에 우선순위 스케줄러(priority scheduler)를 구현
 현재 pintos에서 스레드 스케줄러는 round-robin 방식을 채택하고 있습니다. 이 방식은 스레드 간의 우선순위 없
이 ready_list에 들어온 순서대로 실행되지만 제대로 된 우선순위 스케줄링이 이루어지지 않고 있습니다. 라운드로빈
스케줄링은 공정성, 간단한 구현 등 장점들이 존재하나, 이는 우선순위를 고려하지 않기 때문에 중요한 작업에 더 많
은 CPU 시간을 할당하는 것이 어렵고, 스레드의 작업이 긴 경우 스레드 전환 비용이 높아질 수 있는 단점이 있습니
다.
 따라서 본 보고서에서는 이러한 단점들을 극복하기 위해 스케줄링 방식을 Priority 스케줄링 방식으로 개선하고,
pintos가 제공하는 테스트를 통해 구현한 Priority 스케줄링이 제대로 동작하는지 확인하고자 합니다.
