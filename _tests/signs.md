---
layout: default
title: Тест по дорожным знакам
---

<div class="container pt-6 pb-6">
  {% assign test = site.data.tests | where: "id", "signs" | first %}
  
  <h1 class="mb-4 text-center">{{ test.title }}</h1>
  <p class="text-center mb-5">{{ test.description }}</p>

  <div class="quiz">
    {% for question in test.questions %}
      <div class="card p-3 mb-4" data-correct-answer="{{ question.answer | downcase | strip_newlines }}">
        <h2 class="h5">{{ question.question }}</h2>
        {% if question.image %}
          <div class="text-center my-3">
            <img src="{{ question.image | relative_url }}" alt="Знак" class="img-fluid" style="max-height:150px;">
          </div>
        {% endif %}
        <form>
          {% for option in question.options %}
            <div class="form-check">
              <input class="form-check-input" type="radio" name="question{{ forloop.parentloop.index }}" id="q{{ forloop.parentloop.index }}_{{ forloop.index0 }}">
              <label class="form-check-label" for="q{{ forloop.parentloop.index }}_{{ forloop.index0 }}">
                {{ option }}
              </label>
            </div>
          {% endfor %}
        </form>
      </div>
    {% endfor %}
    <div class="text-center">
      <button class="button button-primary mt-4">Проверить результаты</button>
    </div>
  </div>
</div>


<script>
document.addEventListener('DOMContentLoaded', function() {
  const checkButton = document.querySelector('.button-primary');
  checkButton.addEventListener('click', function() {
    let totalQuestions = document.querySelectorAll('.quiz .card').length;
    let correctAnswers = 0;

    document.querySelectorAll('.quiz .card').forEach((card, index) => {
      const selected = card.querySelector('input[type="radio"]:checked');
      const correctAnswer = card.getAttribute('data-correct-answer'); // Correct answer from data-* attribute
      console.log(correctAnswer);
      console.log(selected);

      if (selected) {
        const selectedLabel = selected.nextElementSibling.textContent.trim().toLowerCase(); // Convert to lowercase to avoid case mismatches
        if (selectedLabel === correctAnswer) {
          correctAnswers++;
          selected.closest('.form-check').classList.add('text-success');
        } else {
          selected.closest('.form-check').classList.add('text-danger');
        }

        // Highlight correct answer
        card.querySelectorAll('label').forEach(label => {
          if (label.textContent.trim().toLowerCase() === correctAnswer) {
            label.closest('.form-check').classList.add('text-success');
          }
        });
      }
    });

    alert(`Ваш результат: ${correctAnswers} из ${totalQuestions}`);
  });
});


</script>
