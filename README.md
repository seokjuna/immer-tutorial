immer 사용법 알아보기<br>
<br>
노션 링크: https://seokjuna.notion.site/12-immer-99a6e6d8452f40ecba5d3d14bbd3b775<br>
<br>
immer 사용법
import produce from 'immer';

const nextState = produce(originalState, draft => {
	// 바꾸고 싶은 값 바꾸기
	draft.somewhere.deep.inside = 5;
produce 함수는 두 가지 파라미터를 받음
- 첫 번째: 수정하고 싶은 상태
- 두 번째: 상태를 어떻게 업데이트할지 정의하는 함수
- 두 번째 파라미터로 전달되는 함수 내부에서 원하는 값을 변경하면. produce 함수가 불변성 유지를 대신해 주면서 새로운 상태를 생성해 줌

import produce from 'immer';

const originalState = [
	{
		id: 1,
		todo: '전개 연산자와 배열 내장 함수로 불변성 유지하기',
		checked: true,
	},
	{
		id: 2,
		todo: 'immer로 불변성 유지하기',
		checked: false,
	}
];

const nextState = produce(originalState, draft => {
	// id가 2인 항목의 checked 값을 true로 변경
	const todo = draft.find(t => t.id === 2); // id로 항목 찾기
	todo.checked = true;
		// 혹은 draft[1].checked = true;

	// 배열에 새로운 데이터
	draft.push({
	id: 3,
	todo: '일정 관리 앱에 immer 적용하기',
	checked: false,
	});

	// id = 1인 항목을 제거하기
	draft.splice(draft.findIndex(t => t.id === 1), 1);
});
