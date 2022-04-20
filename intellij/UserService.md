```
package com.example.logincode_annotation.Service;

import com.example.logincode_annotation.Dto.UserDto;
import com.example.logincode_annotation.Entity.UserEntity;
import com.example.logincode_annotation.Entity.UserRepository;
import com.example.logincode_annotation.Exception.ConflictException;
import com.example.logincode_annotation.Exception.NotFoundException;

import lombok.RequiredArgsConstructor;

import org.springframework.stereotype.Service;

@RequiredArgsConstructor //초기화 되지않은 fInal필드나, @NonNull이 붙은 필드에 대해 생성자를 생성해 준다. 주로 의존성 주입편의성을 위해서 사용되곤 한다.
@Service //Controller가 Request를 받으면 적절한 Service에 전달하고, 전달 받은 Service는 business logic을 처리한다. Service가 DB에 DAO로 접근하고, 데이터를 DTO로 전달받은 다음, 데이터를 필요에 맞게 가공하여 반환한다.
public class UserService {

    private final UserRepository userRepository;

    public void saveData(UserDto userDto) {

        UserEntity userEntity = UserEntity.builder()
                .name(userDto.getName())
                .pwd(userDto.getPwd())
                .build();

        userRepository.save(userEntity);
    }

    public void findDate(UserDto userDto) {

    }

    public UserDto login(UserDto userDto) {
        UserEntity userEntity = userRepository.findByname(userDto.getName())
                .filter(entity -> entity.getPwd().equals(userDto.getPwd()))
                .orElseThrow(NotFoundException::new);

        return UserDto.builder()
                .name(userEntity.getName())
                .pwd(userEntity.getPwd())
                .build();
    }

    public void exists(String name) {
        if (userRepository.existsByname(name)) {
            throw new ConflictException();
        }
    }
}
```