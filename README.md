## Android Emulator Docker image

### Usage

* Launch, wait and unlock the emulator

        docker run --privileged -v /dev/kvm:/dev/kvm --rm niltonvasques/android-sdk-and-emulator:0.1.5 \
        bash -c "start_emulator && wait_emulator && unlock_emulator"

* Usage with Drone CI

```yml
build:
  image: niltonvasques/android-sdk-and-emulator:0.1.5
  privileged: true
  commands:
    - cp -a /drone/.gradle /root/ && rm -Rf /drone/.gradle
    - start_emulator && wait_emulator
    - ./gradlew check --daemon -PdisablePreDex --stacktrace
    - ./gradlew assembleDebugAndroidTest --daemon -PdisablePreDex --stacktrace
    - unlock_emulator
    - ./gradlew cC --daemon -PdisablePreDex --stacktrace
    - cp -a /root/.gradle /drone/
cache:
  mount:
    - /drone/.gradle
```
