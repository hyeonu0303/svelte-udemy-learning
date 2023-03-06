<script>
	import ContactCard from './ContactCard.svelte';
	import CourseGoal from './CourseGoal.svelte';
	let couseGoal = '';
	let name = 'park';
	let title = '';
	let description = '';
	let age = 25;
	let image = "https://dimg.donga.com/wps/NEWS/IMAGE/2019/12/22/98915688.2.jpg";
	
	
	
	$: uppercaseName = name.toUpperCase();
	/*
	1.name이 바뀔때마다 다시 계산해줌 
	2.changeName에서 name만 바꿔줬는데도 불구하고 대문자로 바뀐이유는
	$: 라벨 표현식의 오른쪽에 name을 사용했기때문이고,
	name을 사용할때마다 $: 다시실행해서 uppercaseName이 동작함
	즉, 동적코드를 재실행해주는부분
	*/
	
	$: console.log(name);
	
	$: if(name == 'Parkhyeonwoo'){
		console.log('its run!');
		age = 24;
	}
	/*
	change Age버튼을 눌렀을때 if문이 동작하지않는다 왜냐하면
	맨첫줄에있는 의존성만 참조한다는 뜻으로
	if문이 바뀔때에만 의존성에 따라 아래 코드가 실행됨을 알 수 있다.
	변경사항이 있으면 재실행되는 코드를 레이블라벨로 쓸 수 있는거
	
	*/
	function incrementAge() {
		age += 1;
	}
	function changeName(){
		name = 'Parkhyeonwoo';
	}

	function nameInput(event){
		const enteredValue = event.target.value;
		name = enteredValue;
	}
	
	
	/*
	1. 사용자가 과정 목표를 입력할 수 있는 입력필드 추가
	2. 사용자 입력을 h1 태그로 출력합니다
	3. 하나 이상의 느낌표가 포함된 경우 출력을 빨간색으로 색칠합니다(예: 클래스 추가)
	4. h1 태그 + 출력을 사용자 입력을 전달하는 별도의 구성 요소에 넣습니다
	*/
</script>

<style>
	h1 {
		color: purple;
	}
	.highlight {
		color: blue;
	}
</style>

<h1>Hello {uppercaseName}!, my age is {age + 1}</h1>
<button on:click="{incrementAge}">Change Age</button>
<!-- <button on:click={changeName}>Change Name</button> -->
<!-- <input type="text" value="{name}" on:input="{nameInput}"> -->
<input type="text" bind:value="{name}"/>
<!------------------------------------------------------>
<input type="text" bind:value="{title}"/>
<input type="text" bind:value="{image}"/>
<textarea rows="3" bind:value={description}></textarea>
<!--왼쪽은 export한 부분이고 오른쪽은 App.svelte의 변수다-->
<ContactCard userName={name} jobTitle={title} description={description} userImg={image}/>
<input type="text" bind:value={couseGoal} />
<CourseGoal goal={couseGoal}/>
