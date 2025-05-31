Dates and Times
Alright, let's move on to Working with Dates and Times in Java. Handling dates and times correctly is crucial in many applications. Java has evolved its date and time API significantly over the years.
Before Java 8, the primary classes for date and time were in the java.util package: Date and Calendar. However, these classes had several issues, including:
• Mutability: Both Date and Calendar objects are mutable, which can lead to subtle bugs when they are shared.
• Poor Design: The APIs were not very intuitive or consistent. For example, months in Calendar were 0-indexed.
• Lack of Clarity: It wasn't always clear whether a Date object represented a point in time or a date and time.
• Time Zone Handling: Time zone handling was complex and error-prone.

The java.time Package (Java 8 and Later):
Java 8 introduced the java.time package, which provides a comprehensive and well-designed API for working with dates, times, instants, and durations. This new API is immutable, thread-safe, and much more intuitive.

Key Classes in java.time:

• LocalDate: Represents a date (year, month, day) without time or time-zone.

```Java
import java.time.LocalDate;

public class LocalDateDemo {
    public static void main(String[] args) {
        LocalDate today = LocalDate.now();
        System.out.println("Today's date: " + today);

        LocalDate specificDate = LocalDate.of(2023, 10, 26);
        System.out.println("Specific date: " + specificDate);

        int year = today.getYear();
        java.time.Month month = today.getMonth();
        int dayOfMonth = today.getDayOfMonth();
        System.out.println("Year: " + year + ", Month: " + month + ", Day: " + dayOfMonth);

        LocalDate tomorrow = today.plusDays(1);
        LocalDate lastMonth = today.minusMonths(1);
        System.out.println("Tomorrow: " + tomorrow);
        System.out.println("Last month: " + lastMonth);

        boolean isLeap = today.isLeapYear();
        System.out.println("Is " + year + " a leap year? " + isLeap);
    }
}
```

• LocalTime: Represents a time (hour, minute, second, nanosecond) without date or time-zone.

```Java
import java.time.LocalTime;

public class LocalTimeDemo {
    public static void main(String[] args) {
        LocalTime now = LocalTime.now();
        System.out.println("Current time: " + now);

        LocalTime specificTime = LocalTime.of(14, 30, 45);
        System.out.println("Specific time: " + specificTime);

        int hour = now.getHour();
        int minute = now.getMinute();
        int second = now.getSecond();
        int nano = now.getNano();
        System.out.println("Hour: " + hour + ", Minute: " + minute + ", Second: " + second + ", Nano: " + nano);

        LocalTime later = now.plusHours(2).minusMinutes(30);
        System.out.println("Later time: " + later);
    }
}
```

• LocalDateTime: Represents a date-time without a time-zone. It's essentially a combination of LocalDate and LocalTime.

```Java
import java.time.LocalDateTime;

public class LocalDateTimeDemo {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        System.out.println("Current date and time: " + now);

        LocalDateTime specificDateTime = LocalDateTime.of(2024, java.time.Month.DECEMBER, 25, 9, 0, 0);
        System.out.println("Specific date and time: " + specificDateTime);

        LocalDate datePart = now.toLocalDate();
        LocalTime timePart = now.toLocalTime();
        System.out.println("Date part: " + datePart);
        System.out.println("Time part: " + timePart);

        LocalDateTime inFuture = now.plusDays(10).plusHours(5);
        System.out.println("In future: " + inFuture);
    }
}
```

• Instant: Represents a point in time on the UTC timeline. It's often used for machine-readable timestamps.

```Java
import java.time.Instant;
import java.time.temporal.ChronoUnit;

public class InstantDemo {
    public static void main(String[] args) {
        Instant now = Instant.now();
        System.out.println("Current instant (UTC): " + now);

        Instant specificInstant = Instant.ofEpochSecond(1672531200L); // Example: Jan 1, 2023 UTC
        System.out.println("Specific instant: " + specificInstant);

        Instant laterInstant = now.plus(5, ChronoUnit.HOURS);
        System.out.println("Later instant: " + laterInstant);

        long epochSeconds = now.getEpochSecond();
        int nanoSeconds = now.getNano();
        System.out.println("Epoch seconds: " + epochSeconds);
        System.out.println("Nano seconds: " + nanoSeconds);
    }
}
```

• ZonedDateTime: Represents a date-time with a time-zone. It's crucial for handling times in different geographical regions.

```Java
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;

public class ZonedDateTimeDemo {
    public static void main(String[] args) {
        LocalDateTime localDateTime = LocalDateTime.now();
        ZoneId kolkataZone = ZoneId.of("Asia/Kolkata");
        ZonedDateTime kolkataDateTime = ZonedDateTime.of(localDateTime, kolkataZone);
        System.out.println("Kolkata time: " + kolkataDateTime);

        ZoneId newYorkZone = ZoneId.of("America/New_York");
        ZonedDateTime newYorkDateTime = kolkataDateTime.withZoneSameInstant(newYorkZone);
        System.out.println("New York time (same instant): " + newYorkDateTime);

        System.out.println("Available Zone IDs: " + ZoneId.getAvailableZoneIds());
    }
}
```

• OffsetDateTime: Represents a date-time with a time-zone offset from Greenwich/UTC.

```Java
import java.time.LocalDateTime;
import java.time.OffsetDateTime;
import java.time.ZoneOffset;

public class OffsetDateTimeDemo {
    public static void main(String[] args) {
        LocalDateTime localDateTime = LocalDateTime.now();
        ZoneOffset offset = ZoneOffset.of("+05:30"); // India Standard Time offset
        OffsetDateTime offsetDateTime = OffsetDateTime.of(localDateTime, offset);
        System.out.println("Offset date time: " + offsetDateTime);
    }
}
```

• Duration: Represents a time-based amount of time (e.g., "2 hours, 30 minutes").

```Java
import java.time.Duration;
import java.time.LocalDateTime;

public class DurationDemo {
    public static void main(String[] args) {
        LocalDateTime start = LocalDateTime.now();
        LocalDateTime end = start.plusHours(3).plusMinutes(15);
        Duration duration = Duration.between(start, end);
        System.out.println("Duration: " + duration);
        System.out.println("Duration in minutes: " + duration.toMinutes());
    }
}
```

• Period: Represents a date-based amount of time (e.g., "2 years, 3 months, 10 days").

```Java
import java.time.LocalDate;
import java.time.Period;

public class PeriodDemo {
    public static void main(String[] args) {
        LocalDate date1 = LocalDate.of(2020, 1, 1);
        LocalDate date2 = LocalDate.of(2023, 4, 11);
        Period period = Period.between(date1, date2);
        System.out.println("Period: " + period);
        System.out.println("Years: " + period.getYears() + ", Months: " + period.getMonths() + ", Days: " + period.getDays());
    }
}
```

Formatting and Parsing Dates and Times:
The java.time.format package provides classes for formatting and parsing date and time objects. The DateTimeFormatter class is the main class for this purpose.

```Java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

public class DateTimeFormatterDemo {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();

        // Predefined formats
        DateTimeFormatter isoFormatter = DateTimeFormatter.ISO_DATE_TIME;
        System.out.println("ISO format: " + now.format(isoFormatter));

        // Custom format
        DateTimeFormatter customFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        System.out.println("Custom format: " + now.format(customFormatter));

        // Parsing a string to LocalDateTime
        String dateTimeString = "2024-05-18 11:00:00";
        LocalDateTime parsedDateTime = LocalDateTime.parse(dateTimeString, customFormatter);
        System.out.println("Parsed date time: " + parsedDateTime);

        // Localized format
        DateTimeFormatter localizedFormatter = DateTimeFormatter.ofLocalizedDateTime(java.time.format.FormatStyle.MEDIUM).withLocale(Locale.US);
        System.out.println("Localized format (US): " + now.format(localizedFormatter));
    }
}
```

Interoperability with Legacy Date and Time Classes:
The java.time package also provides methods to convert between the new date and time classes and the older java.util.Date and java.util.Calendar classes.
• Date.from(Instant instant): Converts an Instant to a Date.
• date.toInstant(): Converts a Date to an Instant.
• GregorianCalendar.from(ZonedDateTime zdt): Creates a GregorianCalendar from a ZonedDateTime.
• calendar.toZonedDateTime(): Converts a Calendar to a ZonedDateTime.

Key Advantages of java.time:
• Immutability: Objects are immutable, making them thread-safe and reducing the risk of unexpected changes.
• Clearer API: The API is more consistent and easier to understand.
• Better Time Zone Handling: The java.time.ZoneId and java.time.ZonedDateTime classes provide robust time zone support.
• Separation of Concerns: Clear distinction between dates, times, and date-times.
The java.time package is the recommended way to handle dates and times in Java 8 and later. It provides a much-improved API compared to the legacy classes.
