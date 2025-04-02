# Sort by in Spring Data JPA Repository

```java
List<Appointment> findByDoctorIdAndAppointmentDate(Long doctorId, LocalDate date, Sort sort);
```

```java
List<Appointment> appointment = appointmentRepository.findByDoctorIdAndAppointmentDate(
                doctorId, date, Sort.by(Sort.Direction.ASC, "timeSlot"));
```
