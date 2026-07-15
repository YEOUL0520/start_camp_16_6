<template>
  <section class="festivals-page">
    <div class="page-hero">
      <div class="page-copy">
        <span class="hero-kicker">GUMI · GYEONGBUK FESTIVALS</span>
        <h1>구미·경북의 축제와<br />이벤트를 만나보세요</h1>
        <p>시작일과 종료일이 정리된 축제는 달력에 표시되고, 리스트로도 확인할 수 있어요.</p>
      </div>

      <div class="hero-side-card">
        <h2>이번 달의 추천</h2>
        <p>지역의 특별한 행사와 여행 일정을 한눈에 확인해보세요.</p>
      </div>
    </div>

    <div class="calendar-card">
      <div class="section-header">
        <div>
          <h2>축제 캘린더</h2>
          <p>축제 시작일·종료일 기준으로 달력에 일정이 표시됩니다.</p>
        </div>
      </div>

      <FullCalendar :options="calendarOptions" />
    </div>

    <div class="festival-list">
      <article v-for="festival in festivals" :key="festival.id" class="festival-card">
        <div class="festival-content">
          <span class="festival-chip">{{ festival.category || '축제' }}</span>
          <h3>{{ festival.title }}</h3>
          <p>{{ festival.description }}</p>
        </div>

        <div class="festival-meta">
          <span>{{ festival.startDate || festival.date || '일정 미정' }}</span>
          <span v-if="festival.endDate">{{ festival.endDate }}</span>
          <span>{{ festival.location }}</span>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue'
import FullCalendar from '@fullcalendar/vue3'
import dayGridPlugin from '@fullcalendar/daygrid'
import { festivals as mockFestivals } from '../data/homeMock'

const festivals = ref([])

function normalizeDate(value) {
  if (!value) return null
  const text = String(value).trim()

  if (/^\d{4}-\d{2}-\d{2}$/.test(text)) return text
  if (/^\d{4}\.\d{2}\.\d{2}$/.test(text)) return text.replace(/\./g, '-')

  return text
}

const calendarEvents = computed(() =>
  festivals.value.map((festival) => {
    const start = normalizeDate(festival.startDate || festival.start || festival.date)
    const end = normalizeDate(festival.endDate || festival.end || festival.startDate || festival.start || festival.date)

    return {
      id: String(festival.id),
      title: festival.title,
      start,
      end: end && end !== start ? end : undefined,
      backgroundColor: '#168152',
      borderColor: '#096b44',
      textColor: '#fff'
    }
  })
)

const calendarOptions = computed(() => ({
  plugins: [dayGridPlugin],
  initialView: 'dayGridMonth',
  locale: 'ko',
  height: 560,
  headerToolbar: {
    left: 'prev,next today',
    center: 'title',
    right: ''
  },
  eventDisplay: 'block',
  events: calendarEvents.value
}))

onMounted(() => {
  festivals.value = mockFestivals
})
</script>

<style scoped>
.festivals-page {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.page-hero {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 18px;
}

.page-copy,
.hero-side-card,
.calendar-card {
  padding: 28px;
  border: 1px solid var(--line);
  border-radius: 24px;
  background: rgba(255, 255, 255, 0.88);
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

.page-copy h1 {
  margin: 0;
  color: var(--navy);
  font-size: clamp(28px, 3vw, 40px);
  line-height: 1.2;
}

.page-copy p,
.hero-side-card p {
  margin: 12px 0 0;
  color: #5d665e;
  font-size: 15px;
  line-height: 1.7;
}

.hero-side-card h2,
.section-header h2 {
  margin: 0;
  color: var(--navy);
  font-size: 20px;
}

.section-header p {
  margin: 6px 0 0;
  color: #6b736f;
  font-size: 14px;
}

.calendar-card :deep(.fc) {
  font-family: inherit;
}

.calendar-card :deep(.fc-toolbar-title) {
  color: var(--navy);
  font-size: 18px;
}

.calendar-card :deep(.fc-button) {
  background: var(--green-800);
  border-color: var(--green-800);
  color: #fff;
}

.festival-list {
  display: grid;
  gap: 14px;
}

.festival-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
  padding: 20px;
  border: 1px solid var(--line);
  border-radius: 18px;
  background: #fff;
  box-shadow: 0 8px 22px rgba(35, 52, 43, 0.06);
}

.festival-content {
  flex: 1;
}

.festival-chip {
  display: inline-block;
  margin-bottom: 8px;
  padding: 6px 10px;
  border-radius: 999px;
  background: var(--green-100);
  color: var(--green-900);
  font-size: 11px;
  font-weight: 800;
}

.festival-card h3 {
  margin: 0 0 8px;
  color: var(--navy);
  font-size: 20px;
}

.festival-card p {
  margin: 0;
  color: #5d665e;
  line-height: 1.6;
}

.festival-meta {
  display: flex;
  flex-direction: column;
  gap: 6px;
  color: #6b736f;
  font-size: 13px;
  white-space: nowrap;
}

@media (max-width: 700px) {
  .page-hero {
    grid-template-columns: 1fr;
  }

  .festival-card {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>