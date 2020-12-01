// Makes it a valid function for clientside and serverside NodeJS
(function(exports){

  exports.isTasksValid = function(useDeadline, deadline, type, typeId, title, description, tasks) {

    if (!isValidDate(deadline) && useDeadline)
      return {valid: false, message: 'You have entered an invalid date.'}

    const validTypes = ['vm', 'downloadable', 'THM', 'none']
    if(!validTypes.includes(type))
      return {valid: false, message: 'You have chosen an invalid type'}

    if(type != 'none' && typeId.length <= 0)
      return {valid: false, message: 'You have chosen invalid materials.'}

    if(title.length <= 0)
      return {valid: false, message: 'You need to enter a title.'}

    if(description.length <= 0)
      return {valid: false, message: 'You need to enter a description.'}

    // Validate tasks questions.
    let validTaskQuestions = true
    tasks.forEach(function(task) {
      if(task.question.length == 0) {
        validTaskQuestions = false
        return
      }
    })

    if(!validTaskQuestions)
      return {valid: false, message: 'All tasks must have a question answers.'}

    return {valid: true}

  }

  function isValidDate(d) {
    let date = new Date(d)
    return date instanceof Date && !isNaN(date);
  }

  exports.isValidDate = isValidDate

})(typeof exports === 'undefined'? this['validation']={}: exports);
