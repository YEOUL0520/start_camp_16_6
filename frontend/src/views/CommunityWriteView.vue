<template>
  <section class="write-page">
    <div class="write-card">
      <span class="hero-kicker">GUMI · GYEONGBUK COMMUNITY</span>
      <h1>게시글 작성하기</h1>
      <p>여행 경험이나 추천글을 남겨보세요.</p>

      <form class="write-form">
        <label>
          제목
          <input type="text" placeholder="제목을 입력하세요" />
        </label>

        <label>
          카테고리
          <select>
            <option>여행</option>
            <option>맛집</option>
            <option>축제</option>
            <option>자유</option>
          </select>
        </label>

        <label>
          내용
          <textarea rows="8" placeholder="내용을 입력하세요"></textarea>
        </label>

        <button class="btn btn--primary" type="button">게시글 등록</button>
      </form>
    </div>
  </section>
</template>

<style scoped>
.write-page {
  display: flex;
  justify-content: center;
}

.write-card {
  width: 100%;
  max-width: 760px;
  padding: 28px;
  border: 1px solid var(--line);
  border-radius: 24px;
  background: rgba(255,255,255,0.92);
  box-shadow: var(--shadow);
}

.hero-kicker {
  display: inline-block;
  margin-bottom: 12px;
  color: var(--green-700);
  font-size: 11px;
  font-weight: 850;
  letter-spacing: 1.8px;
}

.write-card h1 {
  margin: 0;
  color: var(--navy);
  font-size: clamp(24px, 2.4vw, 30px);
}

.write-card p {
  margin: 8px 0 20px;
  color: #5d665e;
}

.write-form {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.write-form label {
  display: flex;
  flex-direction: column;
  gap: 8px;
  color: var(--navy);
  font-weight: 700;
}

.write-form input,
.write-form select,
.write-form textarea {
  padding: 12px 14px;
  border: 1px solid var(--line);
  border-radius: 12px;
  background: #fff;
}

.write-form textarea {
  resize: vertical;
}
</style>