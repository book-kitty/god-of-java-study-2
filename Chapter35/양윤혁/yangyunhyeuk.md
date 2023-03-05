
> 정리

## @FXML

- 해당 어노테이션을 메서드에 붙이면, 해당 메서드는 onAction을 처리하기 위한 메서드로 인식한다.
- 연동되는 UI 컴포넌트가 어떤 것인지 확인할 때 필요한 ActionEvent 클래스의 객체를 매개 변수로 받는다.
    
    ```jsx
    @FXML
    private void numberButtonAction(ActionEvent event) {}
    ```
